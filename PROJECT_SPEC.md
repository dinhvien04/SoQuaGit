git status xem trạng thái xem có những thay đổi code nào k
git branch là xem danh sách các nhánh và mình đang ở nhánh nào
git branch <tennhanh> là mình thêm 1 nhánh mới 

git add 


git config là lệnh để cấu hình git thiết lập, xem và sửa đổi cấu hình

git config user.name là mình muốn  muốn tra tên và user name từ dinhvien04 thành vien.nguyendinh


muốn chuyển qua từ 1 nhánh này sang nhánh khác

    đầu tiên là xem đang ở nhánh nào

    git branch

    muốn chuyển sang nhánh master 

    git checkout master

khi mà mình muốn gộp nhánh thì
    đầu tiên là mình chuyến về nhánh muốn nhận code
    git checkout master

    tiếp theo là mình muốn merge nhánh khác Vào
    git merge vien.nguyendinh

    push origin master

trường hợp khi mà mình gộp nhánh mà cả 2 nhánh đã push rùi cùng tên mà khác kí tự thì Sao 
    đầu tiên thì sẽ thông báo lỗi Merge Conflict (Xung đột code)
    tiếp theo mình sẽ add, commit, push cái nhánh master lên là được
    (phải xóa cái <<<<<<< HEAD và >>>>>>> vien.nguyendinh là ok )

git reset là dùng để quay lại lịch sử dự án của về 1 thời điểm (commit) trong quá khứ
    
    có 3 mức độ 
        shot
    
    



