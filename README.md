➜  model_test git:(main) ✗ rails c
Loading development environment (Rails 7.1.2)<br>

[1] pry(main)> Entry.all
  Entry Load (0.1ms)  SELECT "entries".* FROM "entries"
+----+----------------------+------------------------+-------------------------+-------------------------+
| id | title                | body                   | created_at              | updated_at              |
+----+----------------------+------------------------+-------------------------+-------------------------+
| 1  | はじめてのエントリー | はじめまして！         | 2024-01-11 09:45:07 UTC | 2024-01-11 09:45:07 UTC |
| 2  | 2番目のエントリー    | おひさしぶりです！     | 2024-01-11 09:46:12 UTC | 2024-01-11 09:46:12 UTC |
| 3  | 3番目のエントリー    | もうくじけました・・・ | 2024-01-11 09:46:52 UTC | 2024-01-11 09:46:52 UTC |
+----+----------------------+------------------------+-------------------------+-------------------------+
3 rows in set<br>

[2] pry(main)> Comment.all
  Comment Load (0.3ms)  SELECT "comments".* FROM "comments"
+----+------------------------+------------+----------+-------------------------+-------------------------+
| id | body                   | status     | entry_id | created_at              | updated_at              |
+----+------------------------+------------+----------+-------------------------+-------------------------+
| 2  | てすてす               | approved   | 1        | 2024-01-11 10:59:57 UTC | 2024-01-11 10:59:57 UTC |
| 3  | どうもどうも           | unapproved | 1        | 2024-01-11 11:00:37 UTC | 2024-01-11 11:00:37 UTC |
| 4  | こんにちはこんにちは！ | approved   | 3        | 2024-01-11 11:10:41 UTC | 2024-01-11 11:10:41 UTC |
+----+------------------------+------------+----------+-------------------------+-------------------------+
3 rows in set<br>

[4] pry(main)> comment = Comment.where(entry_id: 1).select(:id, :body, :status, :entry_id)
  Comment Load (0.1ms)  SELECT "comments"."id", "comments"."body", "comments"."status", "comments"."entry_id" FROM "comments" WHERE "comments"."entry_id" = ?  [["entry_id", 1]]
+----+--------------+------------+----------+
| id | body         | status     | entry_id |
+----+--------------+------------+----------+
| 2  | てすてす     | approved   | 1        |
| 3  | どうもどうも | unapproved | 1        |
+----+--------------+------------+----------+
2 rows in set<br>

[6] pry(main)> entries = Entry.joins(:comments).where(comments: { status: 'unapproved' }).select(:id, :title, :body)
  Entry Load (0.3ms)  SELECT "entries"."id", "entries"."title", "entries"."body" FROM "entries" INNER JOIN "comments" ON "comments"."entry_id" = "entries"."id" WHERE "comments"."status" = ?  [["status", "unapproved"]]
+----+----------------------+----------------+
| id | title                | body           |
+----+----------------------+----------------+
| 1  | はじめてのエントリー | はじめまして！ |
+----+----------------------+----------------+
1 row in set