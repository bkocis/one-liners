It can happen that larger files are added to the commit. Even when the chach is cleared, those large files remain the the index. 

To list out the commits, their size, and path:

```bash
git rev-list --objects --all \
| git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' \
| awk '/^blob/ {print substr($0,6)}' \
| sort --numeric-sort --key=2 \
| cut --complement --characters=13-40 \
| numfmt --field=2 --to=iec-i --suffix=B --padding=7 --round=nearest
```

for example

```bash
da9a7dcca3a1  133MiB pythonEyeknowWebAppA/app/models/conv_lstm_saved_models/model_checkpoint.hdf5
4f8d97475c1a  161MiB pythonEyeknowWebAppA/app/models/person_detection/crowdhuman_yolov5m.pt
6bbc7668b187  165MiB pythonEyeknowWebAppA/app/models/label_fix4/weights/best.pt
d5a962e8fe24  165MiB pythonEyeknowWebAppA/app/models/child_detector_cleaned4/weights/best.pt

```

to remove the large files: 

```bash
git filter-branch -f --index-filter "git rm -rf --cached --ignore-unmatch pythonEyeknowWebAppA/app/models" -- --all
```

after execute the following:

```bash
rm -rf .git/refs/original/
git reflog expire --expire=now --all
git gc --prune=now
git gc --aggressive --prune=now
```

and push to remote:

```bash
git push origin master
```


References:

https://stackoverflow.com/questions/2100907/how-to-remove-delete-a-large-file-from-commit-history-in-the-git-repository

https://www.deployhq.com/git/faqs/removing-large-files-from-git-history

Removing files, folders from cache
https://stackoverflow.com/questions/1274057/how-can-i-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitign
