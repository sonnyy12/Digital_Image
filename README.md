#Tuần 5
Câu 1: Tịnh tiến ảnh và hiệu ứng wave

Bước:
    1. Đọc ảnh: img = Image.open("kiwi.jpg").convert("RGB")

    2. Tính tiến ảnh sang phải 50 và xuống 30:
        x_shift, y_shift = 50, 30
        shifted_img = np.zeros_like(img_np)
        shifted_img[y_shift:, x_shift:] = img_np[:h - y_shift, :w - x_shift]

    3. Tạo sóng:
        Sóng ngang: X_new = X + amplitude * np.sin(2 * np.pi * Y * frequency)
        Sóng dọc: Y_new = Y + amplitude * np.sin(2 * np.pi * X * frequency)

    4. Biến đổi tọa độ mới:
    wave_img = np.zeros_like(shifted_img)
        for i in range(c):
        wave_img[..., i] = map_coordinates(shifted_img[..., i], [Y_new, X_new], order=1, mode='reflect')

    Sử dụng map_coordinates để nội suy giá trị pixel từ ảnh gốc dựa trên tọa độ mới đã bị biến dạng theo hàm sin. Quá trình này được áp dụng cho từng kênh màu R, G, B để tạo hiệu ứng sóng mềm mại trên toàn ảnh.

    5. Lưu ảnh
    6. Hiện thị ảnh trước và sau 

----------------------------------------

Câu 2: 

Bước:
    1. Đọc ảnh
    
    2. Resize cho ảnh trước: ImageOps.contain(image, (max_width, common_height))

    3. Chuyển ảnh sang Numpy để xử lý màu: np.array(image)

    4. Tạo hàm gradient màu: gradient_rgb = (start_rgb + (end_rgb - start_rgb) * gradient)

    5. Áp dụng hàm vào từng ảnh:

    pp_gradient = apply_gradient_color(pp_np, (255, 0, 0), (0, 255, 0))
    wm_gradient = apply_gradient_color(wm_np, (255, 255, 0), (128, 0, 128))

    6. Ghép ảnh liền trong suốt: Image.new("RGBA", (width, height), (0, 0, 0, 0))

    7. Lưu ảnh
    8. Hiển thị ảnh gốc và kết quả

------------------------------------------

Câu 3:

Bước:
    1. Đọc ảnh

    2. Xoay ảnh 45 độ: rotate(image_np, angle=45, reshape=False, mode='reflect')

    3. Chuyển vể ảnh và phản chiếu dọc: ImageOps.mirror(image)

    4. Ghép 2 ảnh lên canva: 
    Image.new("RGB", (width, height), (255, 255, 255))
    canvas.paste(...)

    5. Lưu và hiển thị kết quả

-------------------------------------------

Câu 4:

Bước:
    1. Phóng to ảnh: img.resize((w * 5, h * 5), Image.LANCZOS)
    
    2. Tạo lưới tọa đồ và uốn ảnh bằng hàm sin:
    X_warped = X + amplitude * sin(Y * freq)
    Y_warped = Y + amplitude * sin(X * freq)

    3. Nội suy ảnh tại vị trí tọa độ mới: map_coordinates(image, [Y_warped, X_warped])

    4. Lưu và hiển thị kết quả

