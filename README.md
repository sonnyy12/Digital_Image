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

