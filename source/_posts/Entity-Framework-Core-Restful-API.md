---
title: Entity Framework Core RESTfulAPI
date: 2023-03-07 09:30:09
tags:
---

Database đoạn code sử dụng là MS SqlServer

Lấy string connection: https://www.c-sharpcorner.com/UploadFile/d40a40/get-sql-server-database-connection-string-easily-from-visual/

Lưu ý: Cấp quyền : 'TrustServerCertificate=True'

Program.cs
```c#
// Kết nối tới Sql Server
var connectionString = "Data Source=TAMINHHUY\\SQLEXPRESS;Initial Catalog=QLSINHVIEN;Integrated Security=True;Trusted_Connection=True;TrustServerCertificate=True";
builder.Services.AddDbContext<SinhVienDbContext>(opt => opt.UseSqlServer(connectionString));
```

Model SinhVien.cs trùng khớp dữ liệu với Table SINH_VIEN trong SQL Server:

```cs
using System.ComponentModel.DataAnnotations.Schema;
using System.ComponentModel.DataAnnotations;
using System.Xml.Serialization;

namespace QuanLySinhVien_WebAPI.Models
{
    [Table("SINH_VIEN", Schema = "dbo")]
    public class SinhVien
    {
        [Key]
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        [Column("SINH_VIEN_ID")]
        public int SinhVienId { get; set; }
        [Column("MA_SINH_VIEN")]
        public string MaSinhVien { get; set; }
        [Column("TEN_SINH_VIEN")]
        public string TenSinhVien { get; set; }
        [Column("NGAY_SINH")]
        public DateTime NgaySinh { get; set; }
        [Column("GIOI_TINH")]
        public string GioiTinh { get; set; }
        [Column("KHOA_ID")]
        public int KhoaId { get; set; }
    }
}
```

Và SinhVienController.cs đóng vai trò là service truy vấn tới SQL Server

```cs
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using QuanLySinhVien_WebAPI.Models;

namespace QuanLySinhVien_WebAPI.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class SinhVienController : ControllerBase
    {
        private readonly SinhVienDbContext _sinhVienDbContext;
        public SinhVienController(SinhVienDbContext sinhVienDbContext)
        {
            _sinhVienDbContext = sinhVienDbContext;
        }
        [HttpGet]
        public ActionResult<IEnumerable<SinhVien>> GetSinhViens()
        {
            return _sinhVienDbContext.SinhViens;
        }
        [HttpGet("{sinhVienId:int}")]
        public async Task<ActionResult<SinhVien>> GetById(int sinhVienId)
        {
            var sinhVien = await _sinhVienDbContext.SinhViens.FindAsync(sinhVienId);
            return sinhVien;
        }
        [HttpPost]
        public async Task<ActionResult> Create(SinhVien sinhVien)
        {
            await _sinhVienDbContext.SinhViens.AddAsync(sinhVien);
            await _sinhVienDbContext.SaveChangesAsync();
            return Ok();
        }
        [HttpPut]
        public async Task<ActionResult> Update (SinhVien sinhVien)
        {
            _sinhVienDbContext.SinhViens.Update(sinhVien);
            await _sinhVienDbContext.SaveChangesAsync();
            return Ok();
        }
        [HttpDelete("{sinhVienId:int}")]
        public async Task<ActionResult> Delete(int sinhVienId)
        {
            var sinhVien = await _sinhVienDbContext.SinhViens.FindAsync(sinhVienId);
            _sinhVienDbContext.SinhViens.Remove(sinhVien);
             await _sinhVienDbContext.SaveChangesAsync();
            return Ok();
        }
    }
}
```