# Bài tập Lab1

# CÂU 1:
--
# Đầu tiên là nạp ảnh: 

data = iio.imread('cow.jpg')

# Thực hiện tách 3 màu riêng biệt và lưu ảnh:

red_only = data[:, :, 0]  
iio.imwrite('cow_red_only.jpg', red_only)
# Chỉ hiển thị màu đỏ

green_only = data[:, :, 1]
iio.imwrite('cow_green_only.jpg', green_only)
# Chỉ hiện thị màu xanh lá

blue_only = data[:, :, 2]
iio.imwrite('cow_blue_only.jpg', blue_only)
# Chỉ hiển thị màu xanh dương


# In kết quả:
plt.subplot(1, 3, 1)
plt.imshow(red_only, cmap='Reds')
plt.title("Màu Đỏ")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(green_only, cmap='Greens')
plt.title("Màu Xanh Lá")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(blue_only, cmap='Blues')
plt.title("Màu Xanh Dương")
plt.axis('off')

plt.tight_layout()
plt.show()

---------

# Câu 2:

Hoán đổi các kênh màu (RGB) với nhau
--

1. Nạp ảnh gốc:
img = iio.imread('cow.jpg')

2. Hoán đổi các kênh màu với nhau:

- R <-> G
- R <-> B
- G <-> B

3. Lưu các ảnh sau khi hoán đổi:
4. Hiển thị kết quả 

---------

# Câu 3:

Tăng các giá trị của các kênh màu (h, v, s)
--

1. Nạp ảnh
2. Chuyển đổi màu từ RGB -> HSV 

3. Chỉnh sửa các giá trị màu:
   -Hue: Nhân Hue với chính nó (`h * h`), làm thay đổi tông màu tổng thể của ảnh.
   -Value: Nhân Value lên 1.5 lần (`v * 1.5`), giúp tăng độ sáng tổng thể. Sử dụng `np.clip()` để đảm bảo giá trị không vượt quá 1.
   -Saturation: Nhân Saturation lên 1.5 lần (`s * 1.5`), làm ảnh rực rỡ hơn. Dùng `np.clip()` để tránh tràn giá trị.
4. Chuyển ảnh từ HSV trở lại RGB và lưu thành file `.png` để xem kết quả:
   - `cow_hue.png` cho phần chỉnh Hue.
   - `cow_value.png` cho phần chỉnh Value.
   - `cow_saturation.png` cho phần chỉnh Saturation.
5. Hiển thị kết quả
---------

# Câu 4:

Đổi các giá trị màu ( Hn = 1/3 Ho, Vn = 0,75 Vo)
--
1. Nạp ảnh 
2. Chuyển đổi ảnh từ RGB sang HSV: Dùng `colorsys.rgb_to_hsv` để tách ảnh thành các thành phần Hue (H), Saturation (S) và Value (V).
3. Điều chỉnh giá trị màu:
   -Hue (H): Chia giá trị Hue cho 3 (`h / 3`) giúp thay đổi màu sắc tổng thể của ảnh (ảnh sẽ lệch tông màu).
   -Value (V): Nhân giá trị Value với 0.75 (`v * 0.75`) để làm ảnh tối hơn một chút.
4. Chuyển đổi ảnh từ HSV trở lại RGB: Sử dụng `colorsys.hsv_to_rgb` và lưu lại ảnh mới với tên `cow_modified.png`.
5. Hiển thị kết quả
----------


# Câu 5:

Sử dụng mean filter cho các ảnh
--

## Baby ##

1. Đọc ảnh gốc
2. Tạo bộ lọc trung bình (Mean Filter): Ma trận 5x5 toàn bộ phần tử bằng nhau với tổng bằng 1 (`np.ones((5,5))/25`) để làm mờ ảnh.
3. Áp dụng bộ lọc: Sử dụng hàm `convolve` của `scipy.ndimage` để lọc ảnh với ma trận trung bình, giúp làm mịn ảnh.
4. Lưu ảnh 
5. Hiển thị kết quả

## Flower ##

1. 
2. Tạo bộ lọc trung bình 5x5: Ma trận 5x5, mỗi phần tử bằng 1/25, dùng để làm mờ ảnh.
3. Lọc từng kênh màu riêng biệt: (vì đây là ảnh màu)
  - Áp dụng phép lọc `convolve` với ma trận trung bình lên từng kênh R, G, B.
4. Kết hợp kênh màu lại**: Dùng `np.stack` ghép 3 kênh sau lọc thành ảnh màu mới.
5. Lưu và hiển thị ảnh kết quả**: Ảnh làm mờ được lưu dưới tên `flower_mean_filter.jpeg` và hiển thị ra màn hình.

## Baloons ##

1. 
2. 
3. Lọc từng kênh màu riêng biệt**: Với mỗi kênh màu (R, G, B), áp dụng phép toán `convolve` với kernel trên ảnh, chế độ `same` giữ nguyên kích thước ảnh đầu ra.
4. 