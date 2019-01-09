# Recover a file from git

To restore a deleted file from your repo:

Scenario setup:

```
touch delete.me.recover.me
echo "This is my test file to delete and then restore" >> delete.me.recover.me
git add .
gst
git commit -m "Added test file to recover"
git push
git pull
```

Delete file and sync

```
rm delete.me.recover.me
git add .
gst
git commit -m "Deleted test file"
git push
git pull
```

To recover the file, you need the first 7 digits of the hash header where the file existed, get this from `git log`

```
git log
```

Sample output:

```
commit 8060a55295b84a567a0dc2ff45bc3711c42c42a0 (HEAD -> master, origin/master)
Author: ianbone1 <ianbone1@googlemail.com>
Date:   Tue Jan 8 14:31:45 2019 +0000

    Deleted test file

commit 18b3490ce3cc6379aa4049722969ad1ed412e2f8
Author: ianbone1 <ianbone1@googlemail.com>
Date:   Tue Jan 8 14:31:26 2019 +0000

    Added test file to recover
:
:
```

Need to restore back to the commit beginning 18b3490

```
git checkout 18b3490 -- delete.me.recover.me
git add .
gst
git commit -m "Recovered the delete.me.recover.me file"
git push
```
