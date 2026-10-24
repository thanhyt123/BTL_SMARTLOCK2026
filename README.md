# BTL_SMARTLOCK2026 - An toàn Phần mềm (SoftSec)

> **Môn học:** An toàn phần mềm (CSE703093)  
> **Đề tài:** Giả lập và Kiểm chứng Hình thức Hệ thống Smart Lock IoT (C Simulator & SMT Z3 Verifier)  
> **Nhóm thực hiện:** Group 15  

---

## 📌 Giới thiệu Dự án

Dự án nghiên cứu và triển khai mô hình hệ thống **Smart Lock IoT** viết bằng ngôn ngữ C99, tích hợp các kỹ thuật kiểm chứng hình thức (Formal Verification) và kiểm thử an toàn phần mềm nâng cao nhằm phát hiện sớm các lỗ hổng bộ nhớ và sai sót logic.

### Các điểm nổi bật:
* **C Simulator (520 LOC):** Giả lập hoàn chỉnh cơ chế xác thực PIN, quản lý trạng thái Kripke (`LOCKED`, `UNLOCKING`, `UNLOCKED`, `ALARM`), và bộ đệm ghi nhật ký sự kiện mã hóa XOR.
* **Formal Verification (SMT/BMC):** Tự động hóa kiểm chứng 5 thuộc tính bất biến logic an toàn ($P_1 - P_5$) sử dụng **Z3 SMT Solver** (Python) với độ sâu $k=5$.
* **Kiểm toán & Rà quét Bộ nhớ:** Tích hợp bộ quét mẫu lỗ hổng tự động (`pattern_scanner.py`) và công cụ phân tích động **AddressSanitizer (ASan)** giúp triệt tiêu rò rỉ bộ nhớ ($\text{Memory Drift} = 0 \text{ bytes}$).

---

## 🛠️ Cấu trúc Mã nguồn (Repository Structure)

```text
BTL_SMARTLOCK2026/
├── BaocaoAnToanPhanMem2026.docx    # Báo cáo thuyết minh Word hoàn chỉnh (44 trang)
├── BaocaoAnToanPhanMem2026.pdf     # Bản xuất PDF báo cáo
├── BTL_SMARTLOCK2026.zip           # Lưu trữ đóng gói toàn bộ mã nguồn & báo cáo
├── include/                  # Các tệp khai báo Header (.h)
│   ├── lock_auth.h           # Module xác thực mã PIN / RFID
│   ├── lock_logger.h         # Module ghi nhật ký hoạt động hệ thống
│   └── smart_lock.h          # Cấu trúc dữ liệu và API điều khiển Smart Lock
├── src/                      # Mã nguồn C Simulator
│   ├── 1lock_system.c        # Mã nguồn C mô phỏng gốc (Chứa lỗi bộ nhớ)
│   ├── lock_system_patched.c # Mã nguồn C đã được vá bảo mật (Patched)
│   ├── lock_auth.c           # Xử lý logic xác thực người dùng
│   ├── lock_logger.c         # Xử lý ghi log vào bộ nhớ đệm
│   └── main.c                # Điểm vào chính của trình mô phỏng
├── verifier/                 # Trình kiểm chứng hình thức & Script Python
│   ├── 1check_z3.py          # Kiểm chứng hình thức lỗi bộ nhớ bằng Z3 SMT Solver
│   ├── kripke_bmc.py         # Kiểm chứng Bounded Model Checking dựa trên Kripke Structure
│   ├── pattern_scanner.py    # Trình quét mẫu mã nguồn tĩnh tự động
│   └── memory_trace_demo.py  # Script mô phỏng dấu vết bộ nhớ
├── results/                  # Kết quả thực nghiệm và nhật ký kiểm thử (IEEE 829)
│   ├── asan_crash.txt        # Nhật ký phát hiện lỗi tràn bộ đệm từ AddressSanitizer
│   ├── cppcheck_result.txt   # Kết quả phân tích tĩnh mã nguồn bằng Cppcheck
│   └── kripke_bmc.log        # Log đầu ra thực thi Bounded Model Checking
├── docs/                     # Tài liệu báo cáo chi tiết
│   └── BaocaoAnToanPhanMem2026.docx # Báo cáo chi tiết 7 chương của dự án
├── Makefile                  # Script tự động hóa biên dịch dự án
└── README.md                 # Tài liệu hướng dẫn sử dụng repository
                   
