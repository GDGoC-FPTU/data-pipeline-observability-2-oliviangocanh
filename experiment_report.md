# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600842
**Name:** Nguyen Ngoc Anh
**Date:** 2026-06-10

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Correct: Laptop la san pham electronics dat nhat sau khi da loai bo du lieu xau |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Sai: Agent bi anh huong boi outlier cuc doan (Nuclear Reactor), cho ket qua khong co y nghia thuc te |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi Agent su dung Garbage Data, no cho ra ket qua hoan toan sai vi du lieu dau vao chua nhieu van de chat luong nghiem trong:

**Duplicate IDs:** Record id=1 xuat hien 2 lan (Laptop va Banana), gay nham lan khi tim kiem theo ID va co the lam lech ket qua thong ke.

**Wrong Data Types:** Record "Broken Chair" co truong `price` la chuoi van ban "ten dollars" thay vi so. Khi Agent goi `idxmax()` tren cot price, lenh nay co the bi loi hoac bo qua record do, dan den ket qua khong day du.

**Extreme Outlier:** Record "Nuclear Reactor" co gia $999,999 - mot gia tri bat thuong khong phan anh thuc te. Vi Agent dung logic chon san pham co gia cao nhat (`idxmax()`), no tu dong chon "Nuclear Reactor" - mot ket qua vo nghia trong thuc te.

**Null Values:** Record "Ghost Item" co id=None va category=None. Du lieu thieu khong the su dung duoc nhung van lam o nhiem tap du lieu, anh huong den cac phep tinh thong ke nhu trung binh, max, min.

Tom lai, garbage data khien Agent di tim gia tri "tot nhat" nhung thuc ra chi la outlier sai lech, khong phan anh insight that su tu du lieu kinh doanh.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y.

Du co prompt tot den dau, neu du lieu dau vao bi nhiem (garbage in, garbage out), Agent se luon cho ra ket qua sai. Trong thi nghiem nay, cung mot cau hoi va cung mot logic Agent, nhung voi Clean Data thi cho ket qua hop ly (Laptop $1200), con voi Garbage Data thi tra ve ket qua vo nghia (Nuclear Reactor $999999). Chat luong du lieu la nen tang cot loi: prompt chi la "cach hoi", con data moi la "nguon thong tin" ma Agent dua vao de tra loi.
