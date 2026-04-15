# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-XXXX
**Name:** Do Thi Thuy Trang
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10/10 | Correct! The agent successfully identified the highest-priced electronics product (Laptop at $1200). |
| Garbage Data (`garbage_data.csv`) | Agent Error: I'm choking on the data! (reduction operation 'argmax' not allowed for this dtype) | 1/10 | Complete failure! Agent crashed because price column contains non-numeric values ("ten dollars" as string). |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

AI Agent không thể xử lý garbage data vì nhiều vấn đề chất lượng dữ liệu:

1. **Wrong Data Types (Loại dữ liệu sai)**: Cột price chứa giá trị string "ten dollars" thay vì số. Khi agent cố gắng tìm max price, nó không thể so sánh các string, dẫn đến lỗi 'argmax not allowed for this dtype'.

2. **Duplicate IDs**: Record ID=1 xuất hiện 2 lần (Laptop và Banana). Điều này gây nhầm lẫn về định danh dự liệu.

3. **Null Values**: Một record có ID = null và category = null, vi phạm constraints logic.

4. **Extreme Outliers**: Nuclear Reactor có giá $999,999 - giá trị bất thường cao giữa các items bình thường.

5. **Price <= 0**: Ghost Item có price = 0, không hợp lệ cho một sản phẩm bán được.

Kết quả: Agent hoàn toàn crash và không thể trả lời câu hỏi. Dữ liệu chất lượng thấp làm agent trở nên vô dụng.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** **CÓ, HOÀN TOÀN ĐÚNG!**

Thí nghiệm chứng minh rằng dữ liệu chất lượng cao là QUAN TRỌNG HƠN prompt đẹp. 

Ngay cả khi prompt rất rõ ràng ("What is the best electronic product?"), nếu dữ liệu bị nhiễm xấu thì:
- Agent không thể xử lý → Crash hoàn toàn (1/10)
- Kết quả sai số → Đáp án không tin cậy
- Hệ thống trở nên vô giá trị

Nhưng với dữ liệu sạch đó lại được validate và transform:
- Agent trả lời chính xác
- Tin cậy 100%
- Hệ thống hoạt động tốt

**Kết luận: Dữ liệu sạch là nền tảng của AI tốt. Không thể xây dựng houses of clay!**
