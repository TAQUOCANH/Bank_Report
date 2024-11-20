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


### Về quy mô
```sql
USE [SAVING-WB2]
-- BÁO CÁO TÌNH HÌNH HUY ĐỘNG VỐN 6 THÁNG ĐẦU NĂM
--Về quy mô
IF object_id('TEMPDB..[#DAUKI]','U') IS NOT NULL DROP TABLE [#DAUKI];
SELECT	
	[DK-TK] = SAVING_ACC_ID
	,[DK-KH] = CUSTID
	,[DK-STARTDATE]= SAVE_DATE 
	,[DK-ENDDATE] = SAVE_END_DATE 
	,[DK-ST] = SAV_AMOUNT
INTO [#DAUKI]
FROM [SAVING-WB2]..SAVING_ACCOUNT AS s
WHERE s.SAVE_DATE <= '2023-12-31' AND s.SAVE_END_DATE > '2023-12-31'



IF object_id('TEMPDB..[#QUYI-PST]','U') IS NOT NULL DROP TABLE [#QUYI-PST];
SELECT	
	[QUYI-PST-TK] = SAVING_ACC_ID
	,[QUYI-PST-KH] = CUSTID
	,[QUYI-PST-STARTDATE]= SAVE_DATE 
	,[QUYI-PST-ENDDATE] = SAVE_END_DATE 
	,[QUYI-PST-ST] = SAV_AMOUNT
INTO [#QUYI-PST]
FROM [SAVING-WB2]..SAVING_ACCOUNT AS s
WHERE s.SAVE_DATE BETWEEN '2024-01-01' AND '2024-03-31'


IF object_id('TEMPDB..[#QUYI-PSG]','U') IS NOT NULL DROP TABLE [#QUYI-PSG];
SELECT	
	[QUYI-PSG-TK] = SAVING_ACC_ID
	,[QUYI-PSG-KH] = CUSTID
	,[QUYI-PSG-STARTDATE]= SAVE_DATE 
	,[QUYI-PSG-ENDDATE] = SAVE_END_DATE 
	,[QUYI-PSG-ST] = SAV_AMOUNT
INTO [#QUYI-PSG]
FROM [SAVING-WB2]..SAVING_ACCOUNT AS s
WHERE s.SAVE_END_DATE BETWEEN '2024-01-01' AND '2024-03-31'


IF object_id('TEMPDB..[#QUYII-PST]','U') IS NOT NULL DROP TABLE [#QUYII-PST];
SELECT	
	[QUYII-PST-TK] = SAVING_ACC_ID
	,[QUYII-PST-KH] = CUSTID
	,[QUYII-PST-STARTDATE]= SAVE_DATE 
	,[QUYII-PST-ENDDATE] = SAVE_END_DATE 
	,[QUYII-PST-ST] = SAV_AMOUNT
INTO [#QUYII-PST]
FROM [SAVING-WB2]..SAVING_ACCOUNT AS s
WHERE s.SAVE_DATE BETWEEN '2024-03-31' AND '2024-06-30'



IF object_id('TEMPDB..[#QUYII-PSG]','U') IS NOT NULL DROP TABLE [#QUYII-PSG];
SELECT	
	[QUYII-PSG-TK] = SAVING_ACC_ID
	,[QUYII-PSG-KH] = CUSTID
	,[QUYII-PSG-STARTDATE]= SAVE_DATE 
	,[QUYII-PSG-ENDDATE] = SAVE_END_DATE 
	,[QUYII-PSG-ST] = SAV_AMOUNT
INTO [#QUYII-PSG]
FROM [SAVING-WB2]..SAVING_ACCOUNT AS s
WHERE s.SAVE_END_DATE BETWEEN '2024-03-31' AND '2024-06-30'


IF object_id('TEMPDB..[#CUOIKI]','U') IS NOT NULL DROP TABLE [#CUOIKI];
SELECT	
	[CK-TK] = SAVING_ACC_ID
	,[CK-KH] = CUSTID
	,[CK-STARTDATE]= SAVE_DATE 
	,[CK-ENDDATE] = SAVE_END_DATE 
	,[CK-ST] = SAV_AMOUNT
INTO [#CUOIKI]
FROM [SAVING-WB2]..SAVING_ACCOUNT AS s
WHERE s.SAVE_DATE <= '2024-06-30' AND s.SAVE_END_DATE > '2024-06-30'




IF object_id('TEMPDB..[#TONGHOP]','U') IS NOT NULL DROP TABLE [#TONGHOP];
SELECT 
    DK.[DK-TK],
    DK.[DK-KH],
    DK.[DK-STARTDATE],
    DK.[DK-ENDDATE],
    DK.[DK-ST],
	Q1_PST.[QUYI-PST-TK],
	Q1_PST.[QUYI-PST-KH],
    Q1_PST.[QUYI-PST-STARTDATE],
    Q1_PST.[QUYI-PST-ENDDATE],
    Q1_PST.[QUYI-PST-ST],
	Q1_PSG.[QUYI-PSG-TK],
	Q1_PSG.[QUYI-PSG-KH],
    Q1_PSG.[QUYI-PSG-STARTDATE],
    Q1_PSG.[QUYI-PSG-ENDDATE],
    Q1_PSG.[QUYI-PSG-ST],
	Q2_PST.[QUYII-PST-TK],
	Q2_PST.[QUYII-PST-KH],
    Q2_PST.[QUYII-PST-STARTDATE],
    Q2_PST.[QUYII-PST-ENDDATE],
    Q2_PST.[QUYII-PST-ST],
	Q2_PSG.[QUYII-PSG-TK],
	Q2_PSG.[QUYII-PSG-KH],
    Q2_PSG.[QUYII-PSG-STARTDATE],
    Q2_PSG.[QUYII-PSG-ENDDATE],
    Q2_PSG.[QUYII-PSG-ST],
	CK.[CK-TK],
	CK.[CK-KH],
    CK.[CK-STARTDATE],
    CK.[CK-ENDDATE],
    CK.[CK-ST]
INTO [#TONGHOP]
FROM [#DAUKI] DK
FULL OUTER JOIN [#QUYI-PST] Q1_PST 
    ON DK.[DK-TK] = Q1_PST.[QUYI-PST-TK]
FULL OUTER JOIN [#QUYII-PST] Q2_PST
    ON DK.[DK-TK] = Q2_PST.[QUYII-PST-TK] 
LEFT JOIN [#QUYI-PSG] Q1_PSG
    ON DK.[DK-TK] = Q1_PSG.[QUYI-PSG-TK] OR Q1_PST.[QUYI-PST-TK] = Q1_PSG.[QUYI-PSG-TK]
LEFT JOIN [#QUYII-PSG] Q2_PSG
    ON DK.[DK-TK] = Q2_PSG.[QUYII-PSG-TK] OR Q1_PST.[QUYI-PST-TK] = Q2_PSG.[QUYII-PSG-TK] OR Q2_PST.[QUYII-PST-TK] = Q2_PSG.[QUYII-PSG-TK]
FULL OUTER JOIN [#CUOIKI] CK
    ON DK.[DK-TK] = CK.[CK-TK] OR Q1_PST.[QUYI-PST-TK] = CK.[CK-TK] OR Q2_PST.[QUYII-PST-TK] = CK.[CK-TK];



SELECT
    X.*
FROM 
    (   
        SELECT 
            [STT]           = '1', 
            [Nội dung]      = N'Số khoản tiết kiệm',      
            [12/31/2023]    = COUNT([DK-TK]),            
            [Qúy I Mở Mới]  = COUNT([QUYI-PST-TK]),                                                                                        
            [Qúy I Tất toán]= COUNT([QUYI-PSG-TK]),                                                                                         
            [Qúy II Mở Mới] = COUNT([QUYII-PST-TK]),                                                                                        
            [Qúy II Tất toán]= COUNT([QUYII-PSG-TK]),                                                                                        
            [6/30/2024]     = COUNT([CK-TK])               
        FROM 
            [#TONGHOP] 
        UNION ALL
        SELECT 
            [STT]           = '2', 
            [Nội dung]      = N'Số lượng khách hàng',     
            [12/31/2023]    = COUNT(DISTINCT [DK-KH]),    
            [Qúy I Mở Mới]  = (
                                SELECT COUNT(DISTINCT [QUYI-PST-KH]) 
                                FROM   [#QUYI-PST]  
                                WHERE  [QUYI-PST-KH] NOT IN (SELECT [DK-KH] FROM #DAUKI)
                              ),                                                    
            [Qúy I Tất toán]= (
                                SELECT COUNT(DISTINCT [QUYI-PSG-KH]) 
                                FROM   [#QUYI-PSG] 
                                WHERE  [QUYI-PSG-KH] NOT IN 
                                       (SELECT DISTINCT CUSTID 
                                        FROM   [SAVING-WB2]..SAVING_ACCOUNT 
                                        WHERE  SAVE_DATE <= '2024-04-01' 
                                        AND    SAVE_END_DATE > '2024-04-01')
                              ),     
            [Qúy II Mở Mới] = (
                                SELECT COUNT(DISTINCT [QUYII-PST-KH]) 
                                FROM   [#QUYII-PST] 
                                WHERE  [QUYII-PST-KH] NOT IN 
                                       (SELECT DISTINCT CUSTID 
                                        FROM   [SAVING-WB2]..SAVING_ACCOUNT 
                                        WHERE  SAVE_DATE <= '2024-03-31' 
                                        AND    SAVE_END_DATE > '2024-03-31')
                              ),                 
            [Qúy II Tất toán]= (
                                SELECT COUNT(DISTINCT [QUYII-PSG-KH]) 
                                FROM   [#QUYII-PSG] 
                                WHERE  [QUYII-PSG-KH] NOT IN (SELECT [CK-KH] FROM #CUOIKI)
                              ),                               
            [6/30/2024]     = COUNT(DISTINCT [CK-KH])       
        FROM 
            [#TONGHOP] 
        UNION ALL
        SELECT 
            [STT]           = '3', 
            [Nội dung]      = N'Tổng tiền tiết kiệm',     
            [12/31/2023]    = SUM([DK-ST]),               
            [Qúy I Mở Mới]  = SUM([QUYI-PST-ST]),                                                                                         
            [Qúy I Tất toán]= SUM([QUYI-PSG-ST]),                                                                                         
            [Qúy II Mở Mới] = SUM([QUYII-PST-ST]),                                                                                         
            [Qúy II Tất toán]= SUM([QUYII-PSG-ST]),                                                                                         
            [6/30/2024]     = SUM([CK-ST])               
        FROM 
            [#TONGHOP]
    ) X;

```
<img width="860" alt="Screenshot_1" src="https://github.com/user-attachments/assets/6151f1af-e84f-41ef-b6df-224eea934277">






### Các khoản tất toán năm 2024

```sql

SELECT
    X2.*
FROM
    (
        -- Số tiền gốc phải trả
        SELECT 
            [Tiêu Chí] = N'Số tiền gốc phải trả',  
            [Quý I] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 1 THEN SAV_AMOUNT END),
            [Quý II] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 2 THEN SAV_AMOUNT END),
            [Quý III] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 3 THEN SAV_AMOUNT END),
            [Quý IV] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 4 THEN SAV_AMOUNT END)
        FROM 
            [SAVING-WB2]..SAVING_ACCOUNT 
        WHERE 
            [SAVE_END_DATE] BETWEEN '2024-01-01' AND '2024-12-31'
        
        UNION ALL
        
        -- Số tiền lãi phải trả
        SELECT 
            [Tiêu Chí] = N'Số tiền lãi phải trả',  
            [Quý I] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 1 THEN 
                                (SAV_AMOUNT * (INTEREST / 100.0) * DATEDIFF(DAY, SAVING_ACCOUNT.SAVE_DATE, SAVING_ACCOUNT.SAVE_END_DATE) / 365) 
                              END),
            [Quý II] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 2 THEN 
                                 (SAV_AMOUNT * (INTEREST / 100.0) * DATEDIFF(DAY, SAVING_ACCOUNT.SAVE_DATE, SAVING_ACCOUNT.SAVE_END_DATE) / 365) 
                               END),
            [Quý III] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 3 THEN 
                                  (SAV_AMOUNT * (INTEREST / 100.0) * DATEDIFF(DAY, SAVING_ACCOUNT.SAVE_DATE, SAVING_ACCOUNT.SAVE_END_DATE) / 365) 
                                END),
            [Quý IV] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 4 THEN 
                                 (SAV_AMOUNT * (INTEREST / 100.0) * DATEDIFF(DAY, SAVING_ACCOUNT.SAVE_DATE, SAVING_ACCOUNT.SAVE_END_DATE) / 365) 
                               END)
        FROM 
            [SAVING-WB2]..SAVING_ACCOUNT 
        WHERE 
            [SAVE_END_DATE] BETWEEN '2024-01-01' AND '2024-12-31'
        
        UNION ALL
        
        -- Tổng
        SELECT 
            [Tiêu Chí] = N'Tổng',  
            [Quý I] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 1 THEN 
                                SAV_AMOUNT + (SAV_AMOUNT * (INTEREST / 100.0) * DATEDIFF(DAY, SAVING_ACCOUNT.SAVE_DATE, SAVING_ACCOUNT.SAVE_END_DATE) / 365) 
                              END),
            [Quý II] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 2 THEN 
                                 SAV_AMOUNT + (SAV_AMOUNT * (INTEREST / 100.0) * DATEDIFF(DAY, SAVING_ACCOUNT.SAVE_DATE, SAVING_ACCOUNT.SAVE_END_DATE) / 365) 
                               END),
            [Quý III] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 3 THEN 
                                  SAV_AMOUNT + (SAV_AMOUNT * (INTEREST / 100.0) * DATEDIFF(DAY, SAVING_ACCOUNT.SAVE_DATE, SAVING_ACCOUNT.SAVE_END_DATE) / 365) 
                                END),
            [Quý IV] = SUM(CASE WHEN DATEPART(QUARTER, [SAVE_END_DATE]) = 4 THEN 
                                 SAV_AMOUNT + (SAV_AMOUNT * (INTEREST / 100.0) * DATEDIFF(DAY, SAVING_ACCOUNT.SAVE_DATE, SAVING_ACCOUNT.SAVE_END_DATE) / 365) 
                               END)
        FROM 
            [SAVING-WB2]..SAVING_ACCOUNT 
        WHERE 
            [SAVE_END_DATE] BETWEEN '2024-01-01' AND '2024-12-31'
    ) X2;
```

<img width="588" alt="Screenshot_2" src="https://github.com/user-attachments/assets/6eef9d71-775c-48a6-86ed-8f6a29f5bef8">


### Phân loại theo các tiêu chí

```sql

SELECT
		[Phân Loại]=  CASE
						  WHEN SAV_AMOUNT < 1000000000                              THEN    N'Dưới 1 tỷ'
						  WHEN SAV_AMOUNT >=	1000000000	AND SAV_AMOUNT <= 10000000000 THEN    N'Từ 1 đến 10 tỷ'
						  WHEN SAV_AMOUNT >	10000000000 AND SAV_AMOUNT <= 50000000000 THEN    N'Từ 10 đến 50 tỷ'
						  WHEN SAV_AMOUNT >	50000000000	THEN N'TRÊN 50 TỶ'
					  END 
		,[Số khoản tiết kiệm] = COUNT(DISTINCT SAVING_ACC_ID)
		,[Số tiền tiết kiệm]  = SUM(SAV_AMOUNT)
FROM [SAVING-WB2]..SAVING_ACCOUNT
GROUP BY 	CASE
				WHEN SAV_AMOUNT < 1000000000                              THEN    N'Dưới 1 tỷ'
				WHEN SAV_AMOUNT >=	1000000000	AND SAV_AMOUNT <= 10000000000 THEN    N'Từ 1 đến 10 tỷ'
				WHEN SAV_AMOUNT >	10000000000 AND SAV_AMOUNT <= 50000000000 THEN    N'Từ 10 đến 50 tỷ'
				WHEN SAV_AMOUNT >	50000000000	THEN N'TRÊN 50 TỶ'
			END;
```
<img width="378" alt="Screenshot_3" src="https://github.com/user-attachments/assets/6e82a008-5275-44bc-8165-91382107b942">


