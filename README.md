Use master
Go

Create database QuanLyQuanCafe
GO

Use QuanLyQuanCafe
GO
--Table Đăng nhập
CREATE TABLE TaiKhoan
(
	TenDangNhap varchar(100) PRIMARY KEY,
	MatKhau nvarchar(100) not null ,
	LoaiTaiKhoan nvarchar(10) NOT NULL
)
GO
--Nhập dữ liệu cho table đăng nhập
INSERT dbo.TaiKhoan(TenDangNhap, MatKhau,LoaiTaiKhoan) 
VALUES
('admin','c4ca4238a0b923820dcc509a6f75849b', N'Quản lý'),
('PhuQui','c4ca4238a0b923820dcc509a6f75849b', N'Nhân viên'),
('TruongAn','c4ca4238a0b923820dcc509a6f75849b', N'Thủ kho')
GO

--table thông tin nhân viên
CREATE TABLE ThongTinTaiKhoan
(
	id INT IDENTITY(1,1) PRIMARY KEY,
	HoTen NVARCHAR(100) not null,
	SoDienThoai VARCHAR(100) not null,
	DiaChi NVARCHAR(100) not null,
	CMND VARCHAR(100) not null,
	Tuoi INT not null,
	GioiTinh NVARCHAR(100) NOT NULL,
	TenDangNhap varchar(100) NOT NULL,

	FOREIGN KEY (TenDangNhap) REFERENCES dbo.TaiKhoan(TenDangNhap)
	ON DELETE CASCADE
)
GO
--table thông tin nhân viên
SET IDENTITY_INSERT dbo.ThongTinTaiKhoan ON
INSERT dbo.ThongTinTaiKhoan(id,HoTen,SoDienThoai,DiaChi,CMND,Tuoi, GioiTinh, TenDangNhap)
VALUES
(1 ,N'Võ Huy Khang','0848741399', N'Vĩnh long','02092000',20, 'Nam', 'admin')
GO
SET IDENTITY_INSERT dbo.ThongTinTaiKhoan OFF

--Bàn
CREATE TABLE Ban
(
	id INT IDENTITY(1,1) PRIMARY KEY,
	TenBan NVARCHAR(100) NOT NULL,
	TrangThai NVARCHAR(100) NOT NULL
)
GO

--Nhập dữ liệu cho bảng bàn
INSERT dbo.Ban(TenBan, TrangThai )
VALUES  ( N'Bàn 01',N'Trống'),
		( N'Bàn 02',N'Trống'),
		( N'Bàn 03',N'Trống'),
		( N'Bàn 04',N'Trống'),
		( N'Bàn 05',N'Trống'),
		( N'Bàn 06',N'Trống'),
		( N'Bàn 07',N'Trống'),
		( N'Bàn 08',N'Trống'),
		( N'Bàn 09',N'Trống'),
		( N'Bàn 10',N'Trống')
GO
--Bảng Loại sản phẩm
CREATE TABLE LoaiSanPham
(
	id INT IDENTITY(1,1) PRIMARY KEY,
	TenLoaiSanPham NVARCHAR(100) not null ,
	DanhMuc NVARCHAR(100) not null 
)
Go

--Nhập dữ liệu cho loại sản phẩm
INSERT INTO dbo.LoaiSanPham(TenLoaiSanPham,DanhMuc) VALUES  (N'Đồ ăn sáng', N'Món ăn'),(N'Đồ ăn trưa',N'Món ăn' ),(N'Đồ ăn chiều',N'Món ăn' ),(N'Nước',N'Đồ uống'),(N'Khác',N'Khác')
GO

--Nhập sản phẩm
CREATE TABLE SanPham
(
	id INT IDENTITY(1,1) PRIMARY KEY ,
	TenSanPham NVARCHAR(100) not null,
	DonVi NVARCHAR(100) not null,
	idLoai INT not null,
	Gia FLOAT not null,
	HinhAnh varchar(100) DEFAULT 'Khongcohinhanh.jpg'

	FOREIGN KEY (idLoai) REFERENCES dbo.LoaiSanPham(id)
	ON DELETE CASCADE
)
GO

--Nhập dữ liệu cho sản phẩm
INSERT INTO dbo.SanPham(TenSanPham, idLoai,DonVi, Gia,HinhAnh )
VALUES  
( N'Bánh mì thịt',1,N'Đĩa',15000,'banhmithit.jpg'),
( N'Bánh mì trứng',1,N'Đĩa',15000,'banhmitrung.jpg'),
( N'Bò cụng',2,N'Xiên',100000,'bocung.jpg'),
( N'Cafe sữa',2,N'Đĩa',111111,'cafe.jpg'),
( N'Cafe đen',3,N'Phần',87000,'capheden.jpg'),
( N'Hủ tiếu',3,N'Phần',96000,'Hutieu.jpg'),
( N'Sting',4,N'Chai',15000,'Sting.jpg'),
( N'Pepsi',4,N'Chai',18000,'pepsi.jpg')
GO

--Nhập kho
CREATE TABLE Kho
(
	idHang INT IDENTITY(1,1) PRIMARY KEY ,
	TenHang NVARCHAR(100) not null,
	DVT NVARCHAR(100) not null,
	SL INT not null,
	Gia FLOAT not null
)
GO
--Nhập dữ liệu cho kho
INSERT INTO Kho(TenHang,DVT,SL,Gia)
VALUES
(N'Đường',N'Kg',5,500000),
(N'Bột Cafe',N'Kg',5,500000)

--Bản Voucher
Create TABLE Voucher
(
	id VARCHAR(100) NOT NULL,
	TenVoucher NVARCHAR(100) NOT NULL,
	GiamGia INT NOT NULL,
	GiamTien Float NOT NULL,
	HanSuDung Date NOT NULL,
	TrangThai NVARCHAR(100) NOT NULL  
)
--Nhập dữ liệu cho bản g khuyến mãi
INSERT dbo.Voucher(id, TenVoucher, GiamGia,GiamTien,HanSuDung,TrangThai)
VALUES
	('SVIP',N'Giảm 20 % Tổng hóa đơn',20,0,'2022-10-29',N'Đã sử dụng'),
	('ADMINVIPPRO',N'Vì anh là ADMIN sao lại phải mất tiền',100,0,'2022-10-29',N'Chưa sử dụng'),
	('SVIP202020',N'Giảm 20 % Tổng hóa đơn',20,0,'2022-10-29',N'Chưa sử dụng'),
	('VIP200',N'Giảm 200.000 VND Tổng hóa đơn',0,200000,'2022-10-29',N'Chưa sử dụng')
GO
--Bảng Hóa đơn
CREATE TABLE HoaDon
(
	id INT IDENTITY(100,1) PRIMARY KEY,
	ThoiGianVao DateTime not null,
	ThoiGianRa DateTime NULL,	
	idBan INT not NULl,
	TongCong FLOAT DEFAULT 0,
	TienThua FLOAT DEFAULT 0,
	KhuyenMai FLOAT DEFAULT 0,
	VAT FLOAT DEFAULT 0,
	NhanVien NVARCHAR(200) NULl,
	Voucher VARCHAR(100) NULl,
	TrangThai NVARCHAR(100) not NULL
	
	--FOREIGN KEY (idBan) REFERENCES dbo.Ban(id) để tạo khóa chính, trong đó:
--FOREIGN KEY (idBan): là field ở bảng HoaDon
--REFERENCES dbo.Ban(id): là tham chiếu đến field groupid trong bảng Groups
	FOREIGN KEY (idBan) REFERENCES dbo.Ban(id)
)
GO

--Bảng thông tin hóa đơn
CREATE TABLE ThongTinHoaDon
(
	id INT IDENTITY(1000,1) PRIMARY KEY,
	idHoaDon INT not null,	
	idSanPham INT not null, 
	SoLuong INT not null DEFAULT 0 

	FOREIGN KEY (idHoaDon) REFERENCES dbo.HoaDon(id),
	FOREIGN KEY (idSanPham) REFERENCES dbo.SanPham(id)
	ON DELETE CASCADE
)
GO
--bảng loại khuyến mãi
Create TABLE LoaiKhuyenMai
(
	id INT IDENTITY(1,1) PRIMARY KEY,
	TenLoaiKM NVARCHAR(100) NOT NULL,
)
--Nhập Loại khuyến mãi
INSERT dbo.LoaiKhuyenMai(TenLoaiKM)
VALUES
(N'Giảm giá hóa đơn'),
(N'Giảm giá món'),
(N'Tặng món'),
(N'Mua A món B tặng C')
GO

--Bảng Khuyến mãi
Create TABLE KhuyenMai
(
	id INT IDENTITY(1,1) PRIMARY KEY,
	TenKM NVARCHAR(100) NOT NULL,
	GiamGia INT NOT NULL,
	GiamTien Float NOT NULL,
	ToiDa Float DEFAULT 0,
	DieuKien Float DEFAULT 0,
	idSanPham INT NULL,
	idLoaiKM INT NOT NULL,
	TrangThai NVARCHAR(100) NOT NULL

	FOREIGN KEY (idSanPham) REFERENCES dbo.SanPham(id),
	FOREIGN KEY (idLoaiKM) REFERENCES dbo.LoaiKhuyenMai(id)
	ON DELETE CASCADE
)
--Nhập phiếu khuyến mãi
INSERT dbo.KhuyenMai(TenKM, GiamGia,GiamTien,ToiDa,DieuKien,idSanPham,idLoaiKM,TrangThai)
VALUES
	(N'Mừng VN chiến thằng -10% Tổng hóa đơn(tối đa 100k)',10,0,100000,NULL,NULL,1,N'Đang diễn ra'),
	(N'Noel Ấm Áp - Giảm 100k cho hóa đơn trên 1tr',0,100000,100000,1000000,NULL,1,N'Đang diễn ra'),
	(N'Mừng xuân 2020 Giảm giá không giới hạn 5% tổng hóa đơn',5,0,NULL,NULL,NULL,1,N'Đang diễn ra'),
	(N'Giảm 10% Món cá chép om dưa',10,0,NULL,NULL,1,2,N'Không hoạt động')
GO

-- PROCEDURE hiển thị
create PROC USP_GetDsKho
AS
BEGIN
	SELECT  idHang,TenHang,SL,DVT,Gia FROM Kho 
END
GO
--Thêm Thông tin tài khoản
create PROC themThongTinTk
@tenDangNhap varchar(100), @hoTen nvarchar(100), @diaChi nvarchar(100), @cMND VARCHAR(100), @sDT VARCHAR(100), @tuoi INT, @gioiTinh nvarchar(100)
AS
BEGIN
	INSERT INTO dbo.ThongTinTaiKhoan(HoTen, SoDienThoai, DiaChi, CMND, Tuoi, GioiTinh, TenDangNhap)
	VALUES
	( @hoTen,  @sDT, @diaChi, @cMND, @tuoi, @gioiTinh,  @tenDangNhap )
END
GO
--Thêm kho
CREATE proc dbo.USP_InsertDrink1
@TenSanPham nvarchar(100),@DonVi nvarchar(100), @Gia float, @idLoai int
as  
begin
	Insert into dbo.SanPham
	(TenSanPham,DonVi,Gia,idLoai)
	VALUES
	(@TenSanPham, @DonVi,@Gia, @idLoai )
end
GO
--Thêm sản phẩm
create proc dbo.USP_InsertDrink
@TenSanPham nvarchar(100),@DonVi nvarchar(100), @Gia float, @idLoai int, @tenAnh varchar(100)
as  
begin
	Insert into dbo.SanPham
	(TenSanPham,DonVi,Gia,idLoai,HinhAnh)
	VALUES
	(@TenSanPham,@DonVi, @Gia, @idLoai,@tenAnh )
end
GO

--Thêm kho
create PROC themKho
@tenSP nvarchar(100),@SL int,@gia float,@DVT nvarchar(100)
AS
BEGIN
	INSERT INTO dbo.Kho(TenHang,SL,Gia,DVT)
	VALUES(@tenSP, @SL,@gia,@DVT )
END
GO
--Thêm loại sản phẩm
CREATE PROC themLoaiSanPham
@tenLoaiSanPham nvarchar(100),@danhMuc nvarchar(100)
AS
BEGIN
	INSERT INTO dbo.LoaiSanPham(TenLoaiSanPham,DanhMuc)
	VALUES(@tenLoaiSanPham, @danhMuc )
END
GO
--Thêm bàn
CREATE PROC themBan
@tenBan nvarchar(100)
AS
BEGIN
	INSERT INTO dbo.Ban(TenBan,TrangThai)
	VALUES(@tenBan,N'Trống')
END
GO
--xóa bàn
CREATE PROC XoaBan
@tenBan NVARCHAR(100)
as
BEGIN
	DELETE dbo.Ban WHERE TenBan = 11
END
GO
--Xóa sản phẩm
CREATE PROC XoaSp
@TenSanPham NVARCHAR(100)
as
BEGIN
	DELETE dbo.SanPham WHERE TenSanPham = @TenSanPham
END
GO
--Kiểm tra trạng thái thẻ khuyến mãi
create PROC USP_GetDSKM
AS
BEGIN
	SELECT * FROM KhuyenMai Where TrangThai = N'Đang diễn ra'
END
GO
-- hiện mã gì đó ở dưới
create PROC USP_GetDSKMAll
AS
BEGIN
	SELECT * FROM KhuyenMai 
END
GO
--Hiện bàn
CREATE PROC USP_GetTableList
AS
BEGIN
	SELECT * FROM Ban
END
GO
--Hiện sản phẩm
CREATE PROC USP_GetListFood
AS
BEGIN
	SELECT * FROM SanPham
END
GO
--Hiện danh mục
CREATE PROC USP_GetListMonAn
AS
BEGIN
	SELECT * 
	FROM SanPham a, LoaiSanPham b
	WHERE a.idLoai = b.id AND b.DanhMuc = N'Món ăn'
END
GO
--Hiện danh mục
CREATE PROC USP_GetListDoUong
AS
BEGIN
	SELECT * 
	FROM SanPham a, LoaiSanPham b
	WHERE a.idLoai = b.id AND b.DanhMuc = N'Đồ uống'
END
GO
--Hiện danh mục
CREATE PROC USP_GetListKhac
AS
BEGIN
	SELECT * 
	FROM SanPham a, LoaiSanPham b
	WHERE a.idLoai = b.id AND b.DanhMuc = N'Khác'
END
GO

--Hiện
Create PROC USP_GetHoaDon
@idBan INT
AS
BEGIN
	SELECT f.TenSanPham,bi.SoLuong ,f.Gia,f.DonVi,f.Gia*bi.SoLuong AS ThanhTien 
	FROM dbo.ThongTinHoaDon AS bi ,dbo.HoaDon AS b,dbo.SanPham AS f 
	WHERE bi.idHoaDon = b.id AND bi.idSanPham = f.id AND b.TrangThai=N'Chưa thanh toán' AND b.idBan =@idBan
END
GO
--Hiện
CREATE PROC dbo.USP_InBill
@idBan INT
AS
BEGIN
	SELECT ROW_NUMBER() OVER (ORDER BY TenSanPham) AS [STT] ,f.TenSanPham ,bi.SoLuong,f.Gia ,f.Gia*bi.SoLuong AS ThanhTien
	FROM dbo.ThongTinHoaDon AS bi ,dbo.HoaDon AS b,dbo.SanPham AS f 
	WHERE bi.idHoaDon = b.id AND bi.idSanPham = f.id AND b.TrangThai=N'Chưa thanh toán' AND b.idBan = @idBan
END
GO
--Hiện
Create PROC dbo.USP_InBill1
@idHoaDon INT
AS
BEGIN
	SELECT ROW_NUMBER() OVER (ORDER BY TenSanPham) AS [STT] ,f.TenSanPham ,bi.SoLuong,f.Gia ,f.Gia*bi.SoLuong AS ThanhTien
	FROM dbo.ThongTinHoaDon AS bi ,dbo.HoaDon AS b,dbo.SanPham AS f 
	WHERE bi.idHoaDon = b.id AND bi.idSanPham = f.id AND b.TrangThai=N'Đã thanh toán' AND bi.idHoaDon = @idHoaDon
END
GO


--Xóa tài khoản
CREATE PROC XoaTK
@tenDn VARCHAR(100)
AS
BEGIN
	DELETE dbo.ThongTinTaiKhoan WHERE TenDangNhap = @tenDn
	DELETE dbo.TaiKhoan WHERE TenDangNhap = @tenDn 
END
GO
--Hiện
CREATE PROC USP_DangNhap
@TenDangNhap NVARCHAR(100), @MatKhau NVARCHAR(100)
AS
BEGIN
	SELECT * FROM dbo.TaiKhoan WHERE TenDangNhap=@TenDangNhap AND MatKhau =@MatKhau 
END
GO
--Hiện
CREATE PROC themTaiKhoan
@ten varchar(100), @matKhau nvarchar(100), @loai nvarchar(10)
AS
BEGIN
	INSERT INTO dbo.TaiKhoan( TenDangNhap, MatKhau, LoaiTaiKhoan )
	VALUES (@ten, @matKhau, @loai)
END
GO
--Thêm
create PROC USP_InsertBill
@idBan INT,
@TongCong FLOAT
AS
BEGIN
	INSERT INTO dbo.HoaDon (ThoiGianVao, ThoiGianRa, idBan, TongCong, TrangThai) 
	VALUES ( GETDATE(), null, @idBan, @TongCong , N'Chưa thanh toán') 
END
GO
--Sửa
Create PROC USP_UpdateSL
@SoLuong INT,
@idHoaDon INT,
@idSanPham INT
AS
BEGIN
	UPDATE dbo.ThongTinHoaDon SET SoLuong = @SoLuong WHERE  idHoaDon = @idHoaDon AND idSanPham = @idSanPham
END
GO
--Sửa Bill sản phẩm
CREATE PROC USP_InsertBillInfo
@idHoaDon INT,@idSanPham INT , @SoLuong INT
AS
BEGIN

	DECLARE @isExitsBillInfo INT
	DECLARE @foodCount INT = 1
	--DECLARE @SumSL INT = 0

	SELECT @isExitsBillInfo = id,@foodCount = b.SoLuong 
	FROM dbo.ThongTinHoaDon AS b 
	WHERE idHoaDon = @idHoaDon AND idSanPham = @idSanPham

	IF(@isExitsBillInfo >0)
		BEGIN
			DECLARE @newCount INT = @foodCount + @SoLuong
			IF (@newCount > 0)
				UPDATE dbo.ThongTinHoaDon SET SoLuong = @newCount WHERE idSanPham = @idSanPham
			ELSE
				DELETE dbo.ThongTinHoaDon WHERE idHoaDon = @idHoaDon AND idSanPham = @idSanPham
		END
	ELSE 
		BEGIN
			DECLARE @Count INT = @SoLuong
			IF (@Count > 0)
				BEGIN
					INSERT INTO dbo.ThongTinHoaDon
						(idHoaDon,idSanPham,SoLuong )
					VALUES
						( @idHoaDon,  @idSanPham,  @SoLuong)
				END
		END
END
GO
--Loại bỏ dấu tiếng việt _ hình như cho ảnh 
--https://quyetdo289.wordpress.com/2012/11/25/loai-bo-dau-tieng-viet-trong-t-sql/
CREATE FUNCTION [dbo].[fuConvertToUnsign1]
(
 @strInput NVARCHAR(4000)
)
RETURNS NVARCHAR(4000)
AS
BEGIN 
 IF @strInput IS NULL RETURN @strInput
 IF @strInput = '' RETURN @strInput
 DECLARE @RT NVARCHAR(4000)
 DECLARE @SIGN_CHARS NCHAR(136)
 DECLARE @UNSIGN_CHARS NCHAR (136)
 SET @SIGN_CHARS = N'ăâđêôơưàảãạáằẳẵặắầẩẫậấèẻẽẹéềểễệế
 ìỉĩịíòỏõọóồổỗộốờởỡợớùủũụúừửữựứỳỷỹỵý
 ĂÂĐÊÔƠƯÀẢÃẠÁẰẲẴẶẮẦẨẪẬẤÈẺẼẸÉỀỂỄỆẾÌỈĨỊÍ
 ÒỎÕỌÓỒỔỖỘỐỜỞỠỢỚÙỦŨỤÚỪỬỮỰỨỲỶỸỴÝ'
 +NCHAR(272)+ NCHAR(208)
 SET @UNSIGN_CHARS = N'aadeoouaaaaaaaaaaaaaaaeeeeeeeeee
 iiiiiooooooooooooooouuuuuuuuuuyyyyy
 AADEOOUAAAAAAAAAAAAAAAEEEEEEEEEEIIIII
 OOOOOOOOOOOOOOOUUUUUUUUUUYYYYYDD'
 DECLARE @COUNTER int
 DECLARE @COUNTER1 int
 SET @COUNTER = 1
 WHILE (@COUNTER <=LEN(@strInput))
 BEGIN 
 SET @COUNTER1 = 1
 WHILE (@COUNTER1 <=LEN(@SIGN_CHARS)+1)
 BEGIN
 IF UNICODE(SUBSTRING(@SIGN_CHARS, @COUNTER1,1))
 = UNICODE(SUBSTRING(@strInput,@COUNTER ,1) )
 BEGIN 
 IF @COUNTER=1
 SET @strInput = SUBSTRING(@UNSIGN_CHARS, @COUNTER1,1)
 + SUBSTRING(@strInput, @COUNTER+1,LEN(@strInput)-1) 
 ELSE
 SET @strInput = SUBSTRING(@strInput, 1, @COUNTER-1)
 +SUBSTRING(@UNSIGN_CHARS, @COUNTER1,1)
 + SUBSTRING(@strInput, @COUNTER+1,LEN(@strInput)- @COUNTER)
 BREAK
 END
 SET @COUNTER1 = @COUNTER1 +1
 END
 SET @COUNTER = @COUNTER +1
 END
 SET @strInput = replace(@strInput,' ','-')
 RETURN @strInput
END
GO
--chưa sử dụng
Create proc USP_InsertVoucher
@id varchar(100), @TenVoucher Nvarchar(100), @giamGia INT, @giamTien Float, @hanSuDung Date
as
BEGIN
	INSERT INTO Voucher(id,TenVoucher,GiamGia,GiamTien,HanSuDung,TrangThai)
	VALUES(@id,@TenVoucher,@giamGia,@giamTien,@hanSuDung,N'Chưa sử dụng')
END 
GO
-- trạng thái Voucher thêm mã khuyến mãi
create proc dbo.USP_InsertDiscount
@tenKM NVARCHAR(200) , @giamGia INT , @giamTien FLOAT, @toiDa FLOAT, @dieuKien FLOAT,@idLoaiKM INT
as  
begin
	Insert into dbo.KhuyenMai
	(TenKM,GiamGia,GiamTien,ToiDa,DieuKien,idLoaiKM,TrangThai)
	VALUES
	(@tenKM , @giamGia , @giamTien , @toiDa , @dieuKien,@idLoaiKM,N'Đang diễn ra')
end
GO
-- trạng thái Voucher Update mã khuyến mãi
create proc dbo.USP_UpdateDiscount
@tenKM NVARCHAR(200) , @giamGia INT , @giamTien FLOAT, @toiDa FLOAT, @dieuKien FLOAT,@idLoaiKM INT,@idKM INT
as  
begin
	UPDATE dbo.KhuyenMai 
	SET TenKM = @tenKM,GiamGia = @giamGia,GiamTien = @giamTien,ToiDa = @toiDa ,DieuKien = @dieuKien ,idLoaiKM = @idLoaiKM
	WHERE id = @idKM
end
GO
--Xóa sp
Create Proc USP_DeleteSP
@idHoaDon INT, @idSanPham INT
AS
BEGIN
	DELETE dbo.ThongTinHoaDon Where idHoaDon = @idHoaDon AND idSanPham = @idSanPham
END
GO
--Chuyên môn 
Create Proc ChuyenNMon
@idHoaDon INT,@idSanPham INT,@idTableTo INT,@idTableFrom INT
AS
BEGIN
	SELECT * 
	INTO TEMP
	FROM ThongTinHoaDon
	WHERE idHoaDon = @idHoaDon and idSanPham = @idSanPham;

	declare @idBillTo int
	declare @voucher Varchar(100)

	SELECT @voucher = Voucher from HoaDon Where idBan = @idTableFrom and TrangThai = N'Chưa thanh toán'

	SELECT @idBillTo = id from HoaDon Where idBan = @idTableTo and TrangThai = N'Chưa thanh toán'

	if (@idBillTo is null)
	begin
		INSERT INTO HoaDon(ThoiGianVao,idBan,TrangThai,TongCong)
		VALUES(GetDate(),@idTableTo,N'Chưa thanh toán',0)
		SELECT @idBillTo = Max(id) FROM HoaDon WHERE idBan = @idTableTo and TrangThai = N'Chưa thanh toán'
	end
	if (@voucher is not null)
	begin
		UPDATE HoaDon SET Voucher = @voucher Where id =@idBillTo
	end

	UPDATE ThongTinHoaDon SET idHoaDon = @idBillTo WHERE ID IN (SELECT ID from TEMP)
	
	DROP table dbo.TEMP
END
GO
--Bảng thống kê
Create Proc USP_BCTK
@fromDate DateTime,@toDate DateTime
as
begin
	select hd.id,b.TenBan,hd.TongCong,NhanVien 
	from HoaDon hd,Ban b
	WHERE hd.idBan = b.id  AND ThoiGianRa BETWEEN @fromDate and @toDate and hd.TrangThai = N'Đã thanh toán'
end
GO
