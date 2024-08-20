# Các câu lệnh git thường dùng
```
git add .
```
```
git commit -m "nội dung commit"
```
```
git commit --amend -m "thay đổi mô tả của commit gần nhất"
```
```
git push
```
```
git pull
```
# Clone dự án về máy
```
git clone url
```

# Add repo vào dự án vừa tạo
```
git remote add origin https://github.com/hlongho/custom_webview.git
```
# Pull code
```
git pull
```
Lấy code mới về nằm phía dưới
```
git pull --rebase
```
# Lưu dữ liệu tạm 
Lưu các thay đổi mà chưa commit vào bộ nhớ và reset lại ở commit mới nhất
```
git stash
```
lấy thay đổi gần nhất đã lưu ở trên ra sử dụng lại
```
git stash pop
```
# Reset đến commit
Reset hoàn toàn đến 1 commit, không giữ nội dung đang có
```
git reset --hard id_commit
```
reset đến 1 commit và vẫn giữ nội dung đang có
```
git reset --soft id_commit
```
# Chuyển sang nhánh khác
chuyển sang 1 nhánh cụ thể
```
git checkout tên_nhánh
```
Tạo và chuyển sang nhánh mới
```
git checkout -b Tên_nhánh_mới
```
# Merge code
Merge bình thường, tạo thêm 1 commit
```
git merge tên_nhánh
```
Merge và gom các commit lại thành 1
```
git merge --squash tên_nhánh
```
# Quy trình rebase code nhánh Feature sang main
Đứng ở nhánh feature
```
git rebase tên_nhánh_main
```
nếu có xảy ra conflict thì fix, sau đó:
```
git add tên_file
git rebase --continue
```
chuyển sang nhánh main và merge
```
git checkout tên_nhánh_main
git merge
```
# Cherry-pick - lấy 1 hoặc nhiều commit từ nhánh Feature sang nhánh Main
Checkout về nhánh Main
cherry-pick với commit_id được chỉ định ở nhánh Feature
```
git cherry-pick commit_id
```
cherry-pick với vài commit, không liên tục
```
git cherry-pick commit_id1 commit_id3
```
cherry-pick với 1 loạt commit lần lượt cạnh nhau (không bao gồm commit_id1)
```
git cherry-pick commit_id1...commit_id5
```
cherry-pick với 1 loạt commit lần lượt cạnh nhau (bao gồm commit_id1)
```
git cherry-pick commit_id1^..commit_id5
```
# Check code đã thay đổi
```
git diff
```
# Show code 
show last commit
```
git show
```
show commit chỉ định với commit_id
```
git show commit_id
```

# Thay đổi url repository
Kiểm tra URL hiện tại của remote repository
```
git remote -v
```
Thay đổi URL của remote repository
```
git remote set-url origin URL_mới_của_repository
```
Thay đổi URL của remote repository với token trong trường hợp cần clone
```
git remote set-url origin https://<token>@github.com/<username>/<repo>
```
