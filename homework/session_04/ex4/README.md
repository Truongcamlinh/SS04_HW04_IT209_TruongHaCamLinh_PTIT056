# Bài 4 - `.gitignore` và sửa commit bằng `--amend`

**Sinh viên:** Trương Hà Cẩm Linh  
**Mã sinh viên:** PTIT056  
**Môn học:** IT209

## Tình huống

File `credentials.txt` đã bị commit nhầm. Bài thực hành yêu cầu bỏ file khỏi Git index, giữ nguyên bản cục bộ và ngăn file bị thêm lại. Nội dung credentials trong bài chỉ là dữ liệu mô phỏng.

## Thực hiện

Thêm `credentials.txt` và các file rác vào `.gitignore`, sau đó chạy:

```bash
git rm --cached homework/session_04/ex4/credentials.txt
git add homework/session_04/ex4/.gitignore \
        homework/session_04/ex4/README.md
git commit --amend -m "Hoàn thành bài tập bỏ qua file nhạy cảm"
```

`git rm --cached` chỉ ngừng theo dõi file, không xóa file vật lý. `git commit --amend` tạo commit thay thế với nội dung và thông điệp mới.

## Kết quả kiểm tra thực tế

```text
$ test -f homework/session_04/ex4/credentials.txt && echo "File cục bộ vẫn tồn tại"
File cục bộ vẫn tồn tại

$ git ls-files homework/session_04/ex4/credentials.txt
(không có output)

$ git status --short --ignored
!! homework/session_04/ex4/credentials.txt

$ git log -n 1 --pretty=format:'Commit message: %s'
Commit message: Hoàn thành bài tập bỏ qua file nhạy cảm
```

`git status` thông thường không hiển thị `credentials.txt` và working tree sạch.

## Lưu ý bảo mật

Nếu secret thật đã được push, cần đổi secret và làm sạch toàn bộ lịch sử bằng `git filter-repo`. Amend chỉ thay commit gần nhất.

## Ảnh minh chứng

Đề không bắt buộc ảnh. Thư mục `screenshots/` đã được tạo sẵn nếu cần bổ sung ảnh Terminal.
