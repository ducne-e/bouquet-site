# A Bouquet for You — bản dựng lại (thuần HTML/JS)

Dựng lại trang quà tặng hoa "flowerisblooming.com" theo video, gồm 5 màn:
bay xuyên rừng hoa → tia sáng → thẻ phong thư (FROM/FOR) → bảng scrapbook kéo-thả
(polaroid, thẻ cào, thư yin-yang, YouTube, Spotify, Memory map).

## Chạy
Không cần build. Vì có dùng ảnh nên phải chạy qua web server (mở trực tiếp file:// sẽ bị chặn ảnh).

```bash
cd bouquet-site
python3 -m http.server 5173
# mở http://localhost:5173
```

Hoặc dùng Live Server (VS Code).

## Tùy biến nội dung
Mở `index.html`, sửa object `CONFIG` ở đầu thẻ `<script>`:
- `from`, `to`: tên người gửi / người nhận (cũng đọc được từ URL `?from=...&for=...`)
- `message`, `yin`, `yang`: lời nhắn trong thẻ trung tâm
- `photos`: danh sách ảnh polaroid (thay `assets/photoXX.jpg` bằng ảnh thật của anh)
- `youtube.id`: điền video id (vd `dQw4w9WgXcQ`) để nhúng player thật
- `spotify.uri`: điền `track/<id>` để nhúng Spotify thật
- `map.pin`: ảnh hiển thị trên ghim của Memory map

## Ảnh (đều được tạo tự động bằng PIL)
- `gen_flowers.py` → hoa sprite + `field.jpg` (rừng hoa) + `garland.png` + `cluster.png`
- `gen_extras.py` → `envelope.png`, `bouquet.png`, `yinyang.png`, `photo0x.jpg`, `memmap.jpg`


```

Muốn dùng rừng hoa / bó hoa thật đẹp hơn, chỉ cần thay file trong `assets/` cùng tên.

## Tương tác
- Màn intro tự chạy → tới thẻ phong thư.
- **Bấm phong thư** để mở bảng scrapbook.
- **Kéo nền** để di chuyển cả bảng; **kéo từng thẻ** để sắp xếp.
- Thẻ **Scratch me**: cào bằng chuột/ngón tay, cào ~nửa thẻ là tự lộ hết.
- **Giữ ~1.5 s** trên thẻ ảnh cào: hiện lightbox với ảnh (trái) và ghi chú notebook (phải); nền xung quanh mờ như f/2.8. Nhả tay ra ngoài hoặc ✕ / Escape để đóng.
- `photos[].note` trong CONFIG: điền lời chú thích hiện trong phần notebook bên cạnh ảnh.
- Nút ✕ để đóng từng thẻ; +/− để zoom bản đồ.
