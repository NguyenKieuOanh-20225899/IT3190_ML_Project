- file dữ liệu gốc [penguins_lter.csv](penguins_lter.csv)
- Xử lý dữ liệu [Preprocessing.ipynb](../code/Preprocessing.ipynb)
    - [data_remove_spare_columns.csv](data_remove_spare_columns.csv)
        - Xóa 9 cột không phù hợp cho việc dự đoán loài chim cánh cụt:

            studyName, Sample Number: Thông tin nghiên cứu
            Stage, Region: Giá trị đồng nhất
            Date Egg: Có thể tiết lộ loài
            Individual ID: Chủ quan, riêng biệt với mỗi loài
            Comments: Nhiều giá trị NaN
            Clutch Completion: Mất thời gian quan sát
            Island: Có bias về vị trí nghiên cứu
    - Loại bỏ outliers (dữ liệu không có giá trị quan trọng) [data_remove_outliers.csv](data_remove_outliers.csv)
    - Chia tách dữ liệu Train/Test (80/20)
        Phương pháp stratified split:

        Tách riêng 3 loài: Adelie, Chinstrap, Gentoo
        Shuffle ngẫu nhiên mỗi loài
        Lấy 80% đầu cho train, 20% cuối cho test
        Gộp lại và shuffle lần nữa
    -  Tách Features và Labels
        X: các đặc trưng (features)
        y: nhãn loài (labels)
        Lưu thành 4 file: X_train.csv, y_train.csv, X_test.csv, y_test.csv

- Thực hiện trực quan hóa dữ liệu [Data_visualization.ipynb](../code/Data_visualization.ipynb)
    Mục đích:
    Phân tích và hiểu cấu trúc dữ liệu
    Tìm outliers, missing values
    Phân tích phân phối các features
    Tạo các biểu đồ để báo cáo
- Mã hóa và chia tách dữ liệu (Encoding & Splitting)
    File: [Encode.ipynb](../code/Encode.ipynb)
    Các bước:
    Chuyển đổi text features thành numeric (sử dụng hàm changeTextFeatureToNumeric)
    Xử lý NaN values (fillna với mean hoặc 0)
    Chia dữ liệu theo từng loài (Adelie, Chinstrap, Gentoo)
    Shuffle data
    Chia train/test set (thường 80/20)
    Normalization/Standardization
    Lưu các file cuối cùng vào thư mục data:
    train_data.csv, test_data.csv
    X_train.csv, y_train.csv
    X_test.csv, y_test.csv
- Tạo tập Train/Valid/Test (Optional - nếu cần)
    File: [Train_Valid_Test.ipynb](../code/Train_Valid_Test.ipynb)
    Chia dữ liệu thành 3 tập: train, validation, test
    Tạo các subset với số lượng samples khác nhau (50, 110, 170)
    - File gốc ban đầu (3 files)
        train_data.csv          # Tập train (50% dữ liệu)
        valid_data.csv          # Tập validation (20% dữ liệu: 50%→70%)
        test_data.csv           # Tập test (30% dữ liệu: 70%→100%)
    - Các tập train với kích thước khác nhau (5 sizes)
        train_data_50.csv       # 50 mẫu từ train
        train_data_80.csv       # 80 mẫu từ train
        train_data_110.csv      # 110 mẫu từ train
        train_data_140.csv      # 140 mẫu từ train
        train_data_170.csv      # 170 mẫu từ train
    - Files đã xử lý NaN (8 files có đuôi _NaNmean)
        train_data_50_NaNmean.csv
        train_data_80_NaNmean.csv
        train_data_110_NaNmean.csv
        train_data_140_NaNmean.csv
        train_data_170_NaNmean.csv
        test_data_NaNmean.csv
        valid_data_NaNmean.csv
    - Files đã chuẩn hóa (5 files có đuôi _Normalization)
        train_data_50_Normalization.csv
        train_data_80_Normalization.csv
        train_data_110_Normalization.csv
        train_data_140_Normalization.csv
        train_data_170_Normalization.csv
    - Files test và valid tương ứng (10 files)
        train_data_50_test.csv      # Test chuẩn hóa theo mean/std của train_50
        train_data_50_valid.csv     # Valid chuẩn hóa theo mean/std của train_50
        train_data_80_test.csv
        train_data_80_valid.csv
        ...
    - 