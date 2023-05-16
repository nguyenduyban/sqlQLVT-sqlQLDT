--CAU 1

CREATE TABLE LOAIVATU(
madt nchar(3),
magv nchar(3),
phucap float,
tiendo nchar(10),
primary key(madt,magv)
)
-- cau 2

ALTER TABLE THAMGIA  ADD CONSTRAINT FK_MADT
FOREIGN KEY (MADT) REFERENCES DETAI (MADT)
ALTER TABLE THAMGIA  ADD CONSTRAINT FK_MAGV
FOREIGN KEY (MAGV ) REFERENCES GIAOVIEN (MAGV)

--CAU 3
ALTER TABLE giaovien  ADD CONSTRAINT CHECK1
CHECK(getdate())-year(ngaysinh)>25

--cau 4 thêm dữ liệu cho bảng THAMGIA
insert into thamgia(madt,magv,phucap,tiendo)
values ('','011','5000000','0%')

--cau 5 tang 20% kinh phi cho cac de tai tren 15 thang
update DeTai set KinhPhi=KinhPhi*1.2 where datediff(MONTH,ngaybd,ngaykt)>15

-- cau 6 danh sách gv nữ và có ngày sinh trong năm tháng hiện tại
select *
from GIAOVIEN
where Phai like 'Nu' and MONTH(ngaySinh)=MONTH(getdate())

--cau 7 mã gv '004' chưa tham gia
select thamgiadt
from giaovien join thamgiadt on giaovien.magv=thamgiadt.magv
where thamgiadt.magv<>'GV01'

-cau 8 gv ít đề tài nhất gồm magv,hoten,makhoa,soluong đề tài 
select GIAOVIEN.MaGV,HoTen,MaKhoa,count(thamgiadt.maGV)
from GIAOVIEN join ThamGiaDT on GIAOVIEN.MaGV=ThamGiaDT.MaGV
group by GIAOVIEN.MaGV,HoTen,MaKhoa
having count(thamgiadt.maGV) <= all(
select count(thamgiadt.maGV)
from GIAOVIEN join ThamGiaDT on GIAOVIEN.MaGV=ThamGiaDT.MaGV
group by GIAOVIEN.MaGV,HoTen,MaKhoa
)


--cau 9 Các đề tài có kinh phí nhỏ hơn mức kinh phí trung bình các đề do khoa'cntt' quản lý
select *
from detai join khoa on detai.makhoa=khoa.mahoa
where tenkhoa like 'CNTT' and Kinhphi < (select avg(kinh phi) from detai)

--cau 10 TENKHOA,TENTRUONGKHOA,SOLUONG DE TAI QUAN LY
SELECT k2.MaKhoa,k2.tenKhoa,count(detai.MaKhoa) as sl,GIAOVIEN.HoTen as tenTK
from khoa k2 join DeTai on k2.MaKhoa = DeTai.MaKhoa join GIAOVIEN on GIAOVIEN.MaGV=k2.MaTrKh
group by k2.TenKhoa,k2.MaKhoa,GIAOVIEN.HoTen

--cau 11 Lọc makhoa,matrkh,họ tên trk,họ tên GV từng khoa
select k1.makhoa,gv1.hoten as hotentk , k1.matrkh as matk,gv2.hoten as tengv
from khoa k1 join giaovien gv1 on k1.matrkh=gv1.magv,giaovien gv2 join khoa k2 on gv2.makhoa=k2.makhoa
where k1.matrkh=gv1.magv
