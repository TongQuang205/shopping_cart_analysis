Mục tiêu của bài Lab 1 là áp dụng kỹ thuật khai phá luật kết hợp (Association Rule Mining), cụ thể là thuật toán Apriori, để phân tích dữ liệu mua sắm và tìm ra:

Các tập sản phẩm thường được mua cùng nhau

Các luật kết hợp có ý nghĩa giữa các sản phẩm

Hỗ trợ cho việc:

Gợi ý sản phẩm

Bố trí hàng hóa

Phân tích hành vi khách hàng

2. Dữ liệu sử dụng

Bài lab sử dụng bộ dữ liệu Online Retail Dataset, bao gồm thông tin giao dịch bán lẻ:

InvoiceNo: Mã hóa đơn

StockCode: Mã sản phẩm

Description: Tên sản phẩm

Quantity: Số lượng mua

InvoiceDate: Thời gian giao dịch

UnitPrice: Giá sản phẩm

CustomerID: Mã khách hàng

Country: Quốc gia

📌 Dữ liệu ban đầu được lưu tại:

data/raw/online_retail.csv

3. Pipeline xử lý dữ liệu

Toàn bộ quá trình được xây dựng theo pipeline tự động, chạy bằng Papermill, gồm các bước sau:

Bước 1: Làm sạch dữ liệu

Loại bỏ các dòng:

Số lượng ≤ 0

Giá ≤ 0

Thiếu InvoiceNo hoặc Description

Chuẩn hóa kiểu dữ liệu ngày tháng

➡ Kết quả:

data/processed/cleaned_uk_data.csv

Bước 2: Chuẩn bị giỏ hàng (Basket Preparation)

Chuyển dữ liệu sang dạng Invoice × Item

Mã hóa dữ liệu thành dạng Boolean (0/1):

1: có mua sản phẩm

0: không mua

➡ Kết quả:

data/processed/basket_bool.parquet

Bước 3: Khai phá luật kết hợp (Apriori)

Áp dụng thuật toán Apriori

Các tham số chính:

MIN_SUPPORT = 0.05
MAX_LEN = 2


Giảm dữ liệu để phù hợp với giới hạn RAM:

Lọc TOP sản phẩm phổ biến

Giới hạn độ dài tập mục

➡ Kết quả:

data/processed/rules_apriori_filtered.csv

4. Thuật toán Apriori dùng để làm gì?

Thuật toán Apriori được sử dụng để:

Tìm tập mục phổ biến (frequent itemsets) dựa trên ngưỡng support

Sinh ra các luật kết hợp dạng:

{A} → {B}


Đánh giá mức độ hữu ích của luật thông qua các chỉ số:

Support

Confidence

Lift

📌 Trong bài lab, Apriori giúp phát hiện:

Các sản phẩm thường được mua chung

Mối quan hệ giữa các mặt hàng trong giỏ mua sắm

5. Ý nghĩa các chỉ số chính

Support
→ Tỷ lệ giao dịch chứa tập sản phẩm
→ Độ phổ biến của luật

Confidence
→ Xác suất mua B khi đã mua A
→ Mức độ tin cậy của luật

Lift
→ Mức độ liên quan giữa A và B

Lift > 1: quan hệ tích cực

Lift = 1: độc lập

Lift < 1: quan hệ tiêu cực

6. Kết quả chính

Sau khi chạy pipeline, hệ thống thu được:

Các luật kết hợp có:

Support đủ lớn

Confidence cao

Lift > 1

Các luật này có thể dùng để:

Gợi ý sản phẩm mua kèm

Phân tích hành vi mua sắm

Hỗ trợ quyết định kinh doanh

7. Cách chạy toàn bộ bài Lab

Chạy toàn bộ pipeline bằng một lệnh duy nhất:

conda activate shopping_env
python run_papermill.py


➡ Không cần mở từng notebook thủ công.

8. Công nghệ sử dụng

Python

Pandas, NumPy

Mlxtend (Apriori)

Jupyter Notebook

Papermill

Git & GitHub
