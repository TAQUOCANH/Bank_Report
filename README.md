# BÁO CÁO TÌNH HÌNH HUY ĐỘNG VỐN 6 THÁNG ĐẦU NĂM

## DATASET

| COLUMN_NAME     | DATA_TYPE   | DESCRIPTION                                                                 |
|------------------|-------------|-----------------------------------------------------------------------------|
| ID              | int         | Mã định danh duy nhất cho từng bản ghi trong bảng.                          |
| CUSTID          | nvarchar    | Mã định danh của khách hàng sở hữu tài khoản tiết kiệm.                     |
| SAVING_ACC_ID   | nvarchar    | Số tài khoản tiết kiệm của khách hàng.                                      |
| SAVE_DATE       | date        | Ngày khách hàng bắt đầu gửi tiền vào tài khoản tiết kiệm.                   |
| SAVE_END_DATE   | date        | Ngày tài khoản tiết kiệm hết hạn hoặc đáo hạn.                              |
| INTEREST        | numeric     | Lãi suất áp dụng cho tài khoản tiết kiệm (thường tính theo năm).            |
| SAV_AMOUNT      | numeric     | Số tiền gốc mà khách hàng gửi vào tài khoản tiết kiệm.                      |
| INTEREST_VAL    | numeric     | Số tiền lãi tính được dựa trên số tiền gốc và lãi suất.                     |
| TOTAL_VAL       | numeric     | Tổng giá trị bao gồm cả tiền gốc và lãi (SAV_AMOUNT + INTEREST_VAL).        |
| AUTO_EXTEND     | int         | Cờ đánh dấu tài khoản tiết kiệm tự động gia hạn (1 = Có, 0 = Không).        |
| WITHDRAW_DAY    | date        | Ngày khách hàng rút tiền từ tài khoản tiết kiệm.                            |
| SAV_STATUS      | int         | Trạng thái của tài khoản tiết kiệm (0 = Đóng, 1 = Hoạt động, 2 = Đáo hạn). |

