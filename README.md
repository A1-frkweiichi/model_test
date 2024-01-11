- Entry.all
- Comment.all

![スクリーンショット 2024-01-12 0 17 05](https://github.com/A1-frkweiichi/model_test/assets/102509805/1bcda220-5bed-4f8f-96ab-84abb6eccddb)

# 1. Entryのid:1(title:はじめてのエントリー)に紐づくCommentを表示してください。
# $ comment = Comment.where(entry_id: 1).select(:id, :body, :status, :entry_id)

![スクリーンショット 2024-01-12 0 17 44](https://github.com/A1-frkweiichi/model_test/assets/102509805/9fc69314-d561-4e87-8a92-b0d00dc299bc)

# 2. statusがunapprovedであるCommentがあるEntryを表示してください。
# $ entries = Entry.joins(:comments).where(comments: { status: 'unapproved' }).select(:id, :title, :body)

![スクリーンショット 2024-01-12 0 18 10](https://github.com/A1-frkweiichi/model_test/assets/102509805/bcc3c326-a519-41f1-aa99-a096251437a3)
