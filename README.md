#Tuần 5
#Bài tập lab 3

Câu 1: 

Bước:
    1. Đọc ảnh: img = cv2.imread("colorful-ripe-tropical-fruits.jpg")

    2. Xác định tọa độ kiwi (phía trên góc trái):
        x1, x2 = 173, 243
        y1, y2 = 156, 226
    
    3. Tịnh tiến sang phải 30 pixel:
        new_x1 = x1 + 30
        new_x2 = x2 + 30
    
    4. Hiển thị kết quả

--------------------------------------------

Câu 2:

Bước:
    1. Đọc ảnh: img = cv2.imread("colorful-ripe-tropical-fruits.jpg")

    2. Dùng hàm change_hue(region, delta_hue=90) dùng để thay đổi màu sắc (hue) của một vùng ảnh. Nó chuyển ảnh từ không gian màu BGR sang HSV, điều chỉnh tông màu Hue bằng một lượng delta_hue, sau đó chuyển ảnh về lại BGR để sử dụng. Việc thay đổi Hue giúp biến đổi màu sắc của đối tượng mà không làm mất độ sáng hay độ bão hòa ban đầu.

    3. Xác định tọa độ và đổi màu:

    # Đổi màu đu đủ
img_result[340:801, 133:636] = change_hue(img[340:801, 133:636])

    # Đổi màu dưa hấu
img_result[248:936, 1658:1922] = change_hue(img[248:936, 1658:1922])

    4. Hiển thị kết quả

----------------------------------------------

Câu 3:

Bước:
    1. Đọc ảnh: img = cv2.imread("quang_ninh.jpg")

    2. Hàm rotate_image(image, angle) xoay ảnh quanh tâm ảnh một góc bất kỳ (đơn vị độ) bằng OpenCV. Ảnh được xoay với kích thước giữ nguyên, và viền ngoài được xử lý bằng cv2.BORDER_REFLECT để không xuất hiện vùng đen. Hàm sử dụng phép biến đổi affine để thực hiện phép xoay hiệu quả:
    
    def rotate_image(image, angle):
        (h, w) = image.shape[:2]
        center = (w // 2, h // 2)
        M = cv2.getRotationMatrix2D(center, angle, 1.0)
        rotated = cv2.warpAffine(image, M, (w, h), borderMode=cv2.BORDER_REFLECT)
        return rotated

    3. Xác định tọa độ của thuyền và núi: 

    # Núi giữa ảnh
        y1_mountain, y2_mountain = 80, 520
        x1_mountain, x2_mountain = 400, 700

    # Thuyền lớn dưới ảnh
        y1_boat, y2_boat = 400, 550
        x1_boat, x2_boat = 80, 330

    4. Xoay 2 đối tượng 45 độ:
        rotated_mountain = rotate_image(mountain, 45)
        rotated_boat = rotate_image(boat, 45)

    5. Hiển thị kết quả

----------------------------------------------

Câu 4:

Bước:
    1. Đọc ảnh: img = cv2.imread("pagoda.jpg")

    2. Dùng hàm phóng to: 
    def scale_image(image, fx=1.0, fy=1.0):
        return cv2.resize(image, (0, 0), fx=fx, fy=fy, interpolation=cv2.INTER_CUBIC)

    3. Xác định tọa độ ngẫu nhiên của bức ảnh (này làm cho dui ^_^)
        y1, y2 = 200, 400
        x1, x2 = 450, 600

    4. Phóng to ảnh:
        scaled_pagoda = scale_image(pagoda, fx=5, fy=5)

    5. Hiển thị kết quả

---------------------------------------------

Câu 5:

Bước:
    1. 



#Bài tập tăng cường

Câu 1: Tịnh tiến ảnh và hiệu ứng wave

Bước:
    1. Đọc ảnh: img = Image.open("colorful-ripe-tropical-fruits.jpg")

    2. Xác định tọa độ của quả kiwi và tịnh tiến ảnh sang phải 50 và xuống 30:

        y1, y2 = 120, 280
        x1, x2 = 120, 280
        kiwi = data[y1:y2, x1:x2]

        dx = 50
        dy = 30

    3. Tạo sóng:
        Sóng ngang: Xk_new = Xk + amplitude * np.sin(2 * np.pi * Yk * frequency)
        Sóng dọc: Yk_new = Yk + amplitude * np.sin(2 * np.pi * Xk * frequency)

    4. Lưu ảnh
    5. Hiện thị ảnh trước và sau 

----------------------------------------

Câu 2: 

Bước:
    1. Đọc ảnh: data = iio.imread('colorful-ripe-tropical-fruits.jpg')

 #   2.Tạo gradient cho papaya:

    -Chọn vùng đu đủ:
bmg1 = data[350:800, 120:700] — cắt vùng ảnh chứa đu đủ.

    -Tạo dải gradient ngang:
gradient1 = np.linspace(0, 1, w1) — tạo giá trị từ 0 → 1 theo chiều rộng.

    -Chọn màu chuyển:
Từ đỏ ([255,0,0]) sang xanh lá ([0,255,0]).

    -Trộn màu:
(1 - gradient1) * red + gradient1 * green — mỗi cột là màu pha giữa đỏ và xanh lá.

    -Gán gradient cho ảnh:
Duyệt theo chiều ngang, thay màu từng cột papaya_gradient[:, i, :] = grad_colors1[i].

    -Thêm kênh alpha (độ trong suốt):
Nối thêm kênh alpha 255 → papaya_rgba để vùng gradient hỗ trợ trong suốt khi cần.

 #   3. Tạo gradient cho watermelon:

    -Chọn vùng dưa hấu:
bmg2 = data[300:1100, 1600:2500] — cắt vùng ảnh chứa dưa hấu.

    -Tạo dải gradient ngang:
gradient2 = np.linspace(0, 1, w2) — tạo giá trị từ 0 → 1 theo chiều rộng.

    -Chọn màu chuyển:
Từ vàng ([255,255,0]) sang tím ([128,0,128]).

    -Tính màu trộn:
(1 - gradient2) * yellow + gradient2 * purple — mỗi cột mang màu pha giữa vàng và tím.

    -Áp dụng lên vùng dưa hấu:
Lặp qua chiều ngang for i in range(w2) và gán màu gradient cho mỗi cột.

    4. Ghép ảnh lại với nhau lên canva:

    pp_img = Image.fromarray(papaya_rgba, "RGBA")
    wm_img = Image.fromarray(watermelon_rgba, "RGBA")

    canvas_width = pp_img.width + wm_img.width + 20
    canvas_height = max(pp_img.height, wm_img.height)
    background = Image.new("RGBA", (canvas_width, canvas_height), (0, 0, 0, 0))

    5. Hiển thị ảnh (cũng không hiểu sao nó ra ảnh màu kì vậy T_T)

------------------------------------------

Câu 3:

Bước:
    1. Đọc ảnh: data = iio.imread('quang_ninh.jpg')

    2. Xác định tọa độ của quả núi và thuyền:
        bmg1 = data[50:300, 400:700]
        print(data.shape)

        bmg2 = data[450:550, 480:680]
        print(data.shape)

    3. Tạo hàm rotated và mirror (lật và phản chiếu):

        rotated1 = nd.rotate(bmg1, 45, reshape=False)
        rotated2 = nd.rotate(bmg2, 45, reshape=False)

        mirrored1 = rotated1[:, ::-1, :]
        mirrored2 = rotated2[:, ::-1, :]

    4. Cho hiển thị từng ảnh 


-------------------------------------------

Câu 4:

Bước:
    1. Đọc ảnh: data = iio.imread('pagoda.jpg')
    
    2. Tạo hàm zoom (phóng to):

        phongto = nd.zoom(data, (5, 5, 1)) 
        h, w, c = phongto.shape
        X, Y = np.meshgrid(np.arange(w), np.arange(h))

    3. Tạo hiệu ứng uống cong:

        amplitude = 30
        frequency = 0.002

        X_warped = X + amplitude * np.sin(2 * np.pi * Y * frequency)
        Y_warped = Y

        X_warped = np.clip(X_warped, 0, w - 1)
        Y_warped = np.clip(Y_warped, 0, h - 1)

    4. Lưu và hiển thị kết quả

    --------------------###-----------------------------

    
    ----------------------###-------------------------
Lab 4:

Câu 1:
    Bước:
        1. Mở ảnh & Cắt vùng LangBiang:

    img = Image.open('dalat.jpg').convert('RGB')
    x, y, w, h = 0, 0, 500, 350
    langbiang = img.crop((x, y, x + w, y + h))

        2. Tịnh tiến sang phải 100px:

    translated = Image.new('RGB', (w + 100, h))
    translated.paste(langbiang, (100, 0))

        3. Chuyển sang xám:

    gray = translated.convert('L')

        4. Phân ngưỡng Otsu:
    
    a = np.asarray(gray)
    thres = threshold_otsu(a)
    b = a > thres
    result = Image.fromarray((b * 255).astype(np.uint8))

        5. Lưu & Hiển thị:
    
    result.save('lang_biang.jpg')

    plt.imshow(result, cmap='gray')
    plt.axis('off')
    plt.show()

Câu 2:
    Bước: 
        1. Mở ảnh & Cắt vùng Hồ Xuân Hương:

    img = Image.open('dalat.jpg').convert('RGB')

    x, y, w, h = 500, 0, 500, 700
    hxh = img.crop((x, y, x + w, y + h))
        
        2. Xoay 45°:

    rotated = hxh.rotate(45, expand=True)

        3. Chuyển sang xám & Adaptive Threshold:

    gray = rotated.convert('L')
    a = np.asarray(gray)
    b = threshold_local(a, block_size=61, offset=10)

    binary_adaptive = a > b

        4. Lưu & hiển thị:
    
    result = Image.fromarray((binary_adaptive * 255).astype(np.uint8))

    result.save('ho_xuan_huong.jpg')
    plt.imshow(result, cmap='gray')
    plt.axis('off')
    plt.show()

Câu 3:
    Bước:
        1. Mở ảnh & cắt quảng trường lâm viên:

    img = Image.open('dalat.jpg').convert('L')
    x, y, w, h = 1000, 0, 400, 300
    lam_vien = img.crop((x, y, x + w, y + h))

        2. Phân ngưỡng otsu:
    
    a = np.asarray(lam_vien)
    thres = threshold_otsu(a)
    binary = a > thres

        3. Binary Closing:

    s = np.array([[0, 1, 0],
              [1, 1, 1],
              [0, 1, 0]])
    b = nd.binary_closing(binary, structure=s, iterations=50)

        4. Lưu & hiển thị:

    result = Image.fromarray((b * 255).astype(np.uint8))
    result.save('quan_truong_lam_vien.jpg')

    plt.imshow(result, cmap='gray')
    plt.show()

Câu 4:

1. Các chức năng:

    A. geometric_transformation

        1. coordinate_mapping

        Cắt vùng (0,0,400,300) → minh hoạ mapping toạ độ.

        2. Rotate

        Xoay ảnh 45°.

        3. Scale

        Phóng to ảnh 1.5x so với kích thước gốc.

        4. Shift

        Dịch chuyển ảnh 50 pixel theo X & Y.
    
    B. segment

        1. Adaptive_thresholding

        Dùng threshold cục bộ: block size 61, offset 10.

        2. Otsu

        Phân ngưỡng Otsu toàn cục.

        3. Binary_dilation

        Giãn vùng trắng nhị phân.

        4. Binary_erosion

        Xói mòn vùng trắng nhị phân.

2. Cách hoạt động:
    Bước:
        1.  Mở ảnh dalat.jpg → chuyển sang grayscale ('L').

        2. Hiển thị cây menu:

    1. geometric_transformation
        1.1 coordinate_mapping
        1.2 Rotate
        1.3 Scale
        1.4 Shift
    2. segment
        2.1 Adaptive_thresholding
        2.2 Binary_dilation
        2.3 Binary_erosion
        2.4 Otsu

        3. Nhập:

    geo_choice — chọn biến đổi hình học (hoặc bỏ trống)

    seg_choice — chọn phân vùng (hoặc bỏ trống)

        4. Áp dụng:

    Nếu có geo_choice → thực hiện biến đổi.

    Nếu có seg_choice → chạy tiếp phân vùng trên kết quả biến đổi.

        5. Lưu output_result.jpg & hiển thị.






    
    

