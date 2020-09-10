---
layout: post
subtitle: Các chỉ số trong Ecommerce
tags: [metrics, data]
comments: true
bigimg: /img/ecommerce/bg.png
thumbnail: /img/ecommerce/bg.png
---
Theo nhiều người đánh giá, bước đầu tiên cũng là bước quan trọng nhất trong phân tích dữ liệu (data analysis) là **đặt câu hỏi**. Chúng ta cần biết điều gì, cần đánh giá những chỉ số nào để biết được những điều đó. Chỉ khi biết được mình đang giải bài toán gì, và cần phân tích chỉ số gì để trả lời bài toán đó thì ta mới có thể làm những bước như thu thập, sàng lọc, phân tích dữ liệu được.

Tuy nhiên, việc đặt câu hỏi này lại phụ thuộc vào mô hình kinh doanh mà bạn đang làm việc, vì mỗi mô hình kinh doanh lại yêu cầu những chỉ số khác nhau. Và sau khi tự mình tìm hiểu, cũng như trải qua 1 thời gian làm việc trong lĩnh vực này, mình tự thấy chưa có 1 bài viết tiếng việt nào tóm tắt và mô tả được những chỉ số mà chúng ta quan tâm trong mô hình kinh doanh thương mại điện tử (E-commerce).

Vì vậy, mình quyết định viết bài này nhằm tổng hợp những điều mình biết, mình tìm hiểu từ trước đến nay để phần nào trả lời được câu hỏi: trong e-commerce, chúng ta cần quan tâm những chỉ số nào, và tại sao?

____
Hình thức **thương mại điện tử** chủ yếu trên thế giới và cả ở việt nam là kinh doanh, **bán hàng trên các nền tảng trực tuyến**. Khách hàng *đến trang web* của bạn, *tìm kiếm sản phẩm*, và *đặt mua*.

Một số nền tảng thương mại điện tử phổ biến tại Viêt Nam có thể kể đến: Shopee, Tiki, Lazada, thế giới di động, sendo, fpt shop, ...

Điểm chung của các trang trên đó là chúng đều là các nền tảng B2C (từ doanh nghiệp đến cá nhân) và có thể được phân ra làm 2 dạng: Marketplace (những nền tảng đóng vai trò là trung gian, không có kho hàng như Shopee, Tiki, Lazada, ...) và Inventory (những nền tảng có kho hàng, có sản phẩm của chính họ như thế giới di động, fpt shop, ...).

2 dạng này chủ yếu chỉ khác nhau về cách thức lưu trữ hàng hoá còn về cơ chế bán hàng trên web/app của họ không có sự khác biệt đáng kể, vì vậy, dù mô hình kinh doanh của bạn có là dạng nào trong 2 dạng trên thì cũng có thể sử dụng những chỉ số dưới đây.

____
#### Tổng quan
Theo mình, có 4 nhóm chỉ số mà bạn cần quan tâm để đánh giá được nền tảng ecommerce có đang hoạt động ổn không:

1. **Retention**: việc tái sử dụng dịch vụ, web, app, ... của người dùng. Retention có thể là `Repurchase Rate` - tỷ lệ lặp lại hành vi mua hàng của người dùng, hoặc `Churn Rate` - tỷ lệ người dùng rời bỏ nền tảng của bạn. Điểm chung của các chỉ số về Retention là bạn sẽ theo dõi 1 nhóm người dùng xác định (1 cohort) và đánh giá xem nhóm người này tiếp tục sử dụng hay rời bỏ nền tảng của bạn như thế nào trong 1 khoảng thời gian nhất định.

2. **Conversion**: tỷ lệ chuyển đổi. Đây là những chỉ số liên quan đến khả năng chuyển đổi khách hàng từ bước A đến bước B trong luồng người dùng của bạn. Nó có thể là tỷ lệ chuyển đổi của các kênh marketing, hoặc của từng bước trong luồng của web/app.

3. **Cost**: chi phí. Chi phí ở đây có thể là chi phí để tìm kiếm 1 khách hàng (`CAC - Customer acquisition cost`) hoặc chi phí trên từng đơn hàng (Cost per Order). Về cơ bản, nó là chi phí mà bạn phải bỏ ra trên 1 đơn vị, bạn cần biết thông số này để so sánh nó với giá trị bạn mang lại, và từ đó đánh giá được mô hình của bạn đang hoạt động có mang lại lợi nhuận hay không.

4. **Revenue**: doanh thu. Có chi phí thì tất nhiên phải quan tâm đến doanh thu. Revenue ở đây cũng tính trên 1 đơn vị, có thể là `Customer Lifetime Value - CLV` cho ta biết 1 khách hàng sẽ mang lại bao nhiêu doanh thu trong suốt vòng đời sử dụng. Hoặc có thể tính Average order value, giá trị đơn hàng trung bình để biết trung bình 1 đơn hàng, bạn sẽ có doanh thu bao nhiêu.

Trong mỗi nhóm chỉ số trên, mình sẽ chỉ lấy ra 1 chỉ số mà mình cảm thấy quan trọng và cần thiết nhất, tuỳ trường hợp mô hình kinh doanh của bạn, chỉ số bạn quan tâm có thể sẽ khác.

____
#### Repurchase Rate RR
Đối với Retention, mình quyết định chọn Repurchase Rate là chỉ số chính vì hành vi mua hàng là hành vi quan trọng nhất của nền tảng và chỉ số này cũng giúp ta xác định tỷ lệ khách hàng cũ, mới và từ đó hỗ trợ việc đưa ra chiến lược.

Nền tảng của bạn có thể chú trọng vào tìm kiếm khách hàng mới (**Acquisition**) hay tập trung vào khách hàng cũ (**Loyalty**). Tất nhiên, bạn cũng có thể đồng thời làm cả 2 việc trên (**Hybrid**).

Theo nhìn nhận chủ quan của mình, hầu hết các start-up trong lĩnh vực này sẽ khởi đầu bằng Acquisition, họ cố gắng kéo càng nhiều khách hàng mới càng tốt. Sau đó, khi đã có 1 số lượng khách hàng trung thành nhất định, sẽ là trạng thái Hybrid, vừa chăm sóc khách hàng cũ, vừa duy trì các chương trình thu hút khách mới (như những chương trình khuyến mãi cho người dùng mới trên Shopee, Tiki, Lazada, ...).
Cuối cùng, khi nền tảng của bạn trở nên khủng bố và kiểu chả cần nói ai cũng biết như Amazon, bạn sẽ tập trung cho chương trình Loyalty (như Amazon).

Tuy nhiên, có 1 cách cụ thể hơn để xác định nền tảng của bạn đang ở trạng thái nào và từ đó bạn có thể đưa ra những chiến lược cụ thể. Ví dụ nếu phần lớn khách hàng của bạn là khách hàng mới, thì bạn có thể cân nhắc việc phân bổ nguồn lực và mở rộng việc acquisition *"có vẻ đang hiệu quả này"* của bạn hoặc chuyển sang tăng sự trung thành của khách hàng với web/app, tất cả phụ thuộc và chiến lược của cụ thể của bạn. Mấu chốt là xác định mình đang ở trạng thái nào trong những trạng thái trên.

Ví dụ, trong database của bạn có 1 bảng thống kê đơn hàng như sau

| order_id       | username | order_completed_at |first_order_at | 30_days_since_first | is_30day_RR | 
| ---------- |---------|----------|----------|----------|----------|
|71 | Cuong | 2020-07-06 10:23:54| July 2020 | **2020-08-05**| false
|72 | Long | 2020-07-08 11:24:35| July 2020 | **2020-08-07**| false
|73 | Hoang | 2020-07-27 11:25:35| July 2020 | **2020-08-26**| false
|101 | Cuong | 2020-08-02 10:23:54| July 2020 | 2020-08-05| `true`
|102 | Hoang | 2020-08-25 11:22:35| July 2020 | 2020-08-26| `true`
|103 | Cuong | 2020-09-09 04:20:54| July 2020 | 2020-08-05| false
|104 | Long | 2020-09-09 14:22:35| July 2020 | 2020-08-07| false

Bảng trên đã được xử lý để cho chúng ta có thể xác định được **cohort** - 1 tập khách hàng có chung 1 hành vi xác định. Ở đây, là những **khách hàng có đơn hàng đầu tiên vào tháng 7 năm 2020**. Nói cách khác, đó là những *khách hàng mới* mà chúng ta kiếm được *trong tháng 7*, và ghi nhận tất cả các đơn hàng thành công của họ từ lúc bắt đầu (tháng 7) cho đến hiện tại.

Trong số những khách hàng này (3 người), chỉ có 2 người thực hiện 1 đơn hàng khác trong vòng 30 ngày kể từ ngày đầu tiên mua hàng. Để xác định điều đó, chỉ cần so sánh `order_completed_at` với `30_days_since_first`, nếu nhỏ hơn thì đó là 1 đơn hàng được thực hiện trong vòng 30 ngày từ ngày đầu tiên mua.

Như vậy, ta có thể nói **30-day repurchase rate** hay **30 days RR** là `2/3 = 66.6%`

Tương tự, ta có thể tính **15, 30, 90 days RR** - **tỷ lệ khách hàng mua lại trong 15, 30 hay 90 ngày**, tuỳ vào từng trường hợp kinh doanh cụ thể của bạn.   

`Lưu ý:` là RR là 1 tỷ lệ phụ thuộc vào 2 khoảng thời gian, như trường hợp trên là 30 days RR của *tháng 7*, nếu bạn tính cho các tháng khác, hoặc *cohort* của 1 khoảng thời gian khác (tuần, quý, năm, ...) thì kết quả sẽ ra khác.

Tỷ lệ này cho chúng ta biết, tỷ lệ khách hàng vẫn còn *trung thành* với sản phẩm của mình. Nếu tỷ lệ này lớn, trên `30%`, thì nền tảng ecommerce đang ở trạng thái Loyalty, từ `15%` đến `30%` thì là Hybrid, còn dưới `15%`, thì bạn đang ở trạng thái Acquisition.

____
#### Conversion Rate

Tỷ lệ chuyển đổi Conversion Rate là 1 chỉ số đơn giản nhưng được sử dụng rất đa dạng. Về cơ bản, ban có thể tính tỷ lệ chuyển đổi khách hàng từ bước A đến bước B, với bước A và B có thể là bất cứ bước nào trong luồng người dùng (**user flow**) của bạn. 

Ví dụ khách hàng mở app của bạn lên (A), tìm kiếm sản phẩm, thêm vào giỏ hàng (B). Như vậy ta có thể tính trong 100 khách hàng mở app, có bao nhiêu người sẽ đi đến bước thêm vào giỏ hàng.

`CR từ A đến B = số người ở bước B / số người ở bước A`

Để biết được bạn cần tính **CR** cho bước A nào, B nào, bạn cần xác định rõ `user flow` của mình.  

Nếu mô hình của bạn tập trung vào `acquisition`, có thể bạn sẽ chấp nhận 1 mức CR *thấp hơn* 1 mô hình tập trung vào `loyalty`.  

Với acquisition, bạn thậm chí sẽ tập trung vào CR của các kênh marketing hơn là CR của luồng người dùng sử dụng trên web/app của bạn, vì bạn sẽ muốn biết kênh marketing nào hiệu quả nhất để tìm kiếm người dùng mới.

Vì vậy, xác định **RR** trước và có chiến lược tập trung vào từng loại sẽ xác định mức **CR** chấp nhận được của nền tảng của bạn.

____
#### Customer Acquisition Cost (CAC)

**CAC** được tính bằng việc lấy chi phí bỏ ra chia cho số lượng khách hàng mới thu về được trong 1 khoảng thời gian.

`CAC (trong 1 khoảng thời gian) = Tổng chi phí (marketing, sale, vận hành, ...) liên quan đến tìm kiếm khách hàng / Số người dùng mới`

Tất nhiên, CAC đối với từng doanh nghiệp, mô hình khác nhau sẽ có những tiêu chuẩn khác nhau. Nếu mô hình acquisition, thì CAC có thể sẽ cao vì bạn tập trung vào việc tìm kiếm khách hàng mới, còn nếu loyalty, thì CAC được kỳ vọng sẽ thấp hơn.

____
#### Lifetime Value (CLV hoặc LTV)

**LTV** là doanh thu mà 1 khách hàng tạo ra trong vòng đời của khách hàng.

Vậy vòng đời khách hàng là gì?

Vòng đời khách hàng là thời gian trung bình của 1 khách hàng từ lúc mua hàng lần đầu đến khi không còn mua nữa.

$$
Lifespan = \frac{\text{Tổng thời gian từ lúc mua đến khi không mua nữa}}{\text{Số lượng khách hàng}}
$$

Tất nhiên, việc thống kê thời gian từ lúc mua hàng đến lúc không còn mua nữa của 1 khách hàng có thể là 1 việc rất khó khăn, có khi thời gian này là vài năm thì bạn không thể chờ vài năm để tính nó được.

Có 1 cách để ước lượng giá trị này là dựa vào `Churn Rate`.

**Churn Rate** là tỷ lệ người không tiếp tục mua hàng trên nền tảng của bạn nữa (thực thế Churn có thể tính cho bất kỳ hành động nào, nhưng ở đây ta xét hành động mua hàng).

Cơ bản thì churn rate tính giống như với RR ở trên, cũng đều dựa vào *cohort*. Nó cũng cần 1 đơn vị thời gian để xác định, tuỳ từng công ty mà có thể là churn rate theo tuần, tháng hay năm ...

Ở đây, mình xét **churn rate** theo tháng, tương tự như với 30 day RR xét ở trên, ta tìm ra số người thực hiện **mua hàng lần đầu vào tháng 7**, sau đó đến tháng 8, ta sẽ tính xem **trong số những người mua vào tháng 7**, **ai vẫn còn mua hàng tiếp trong tháng 8**.

$$
Churn Rate = 1 - \frac{\text{tổng số người mua hàng tháng trước và tháng này}}{\text{tổng số người mua hàng tháng trước}}
$$

Giả sử có 100 người mua hàng vào tháng 7, trong số 100 người này, có 25 người đến tháng 8 vẫn mua tiếp, thì **Churn Rate = 75%**, ta có thể nói là có 75% người dùng đã không tiếp tục mua hàng vào tháng tiếp theo.

Từ đây có thể ước lượng

$$
Average Lifespan = \frac{1}{\text{Churn Rate}}
$$

Nếu churn rate tính theo tháng, thì AL cũng sẽ tính theo tháng, như trên thì monthly churn rate là 75%, vậy AL là 100/75 = 1.3 tháng.

Sau khi tính được thời gian trung bình 1 khách hàng sử dụng nền tảng, ta tính giá trị trung bình mà 1 khách hàng mang lại cho chúng ta.

$$
\text{Giá trị trung bình của đơn hàng} = \frac{\text{Tổng doanh thu}}{\text{Tổng số đơn hàng}}
$$

Sau đó, tính số đơn hàng trung bình của 1 khách, để tính được giá trị mà 1 khách mang lại:

$$
\text{Số đơn hàng trung bình của 1 khách} = \frac{\text{Tổng số đơn}}{\text{Tổng số khách}}
$$

Lưu ý là doanh thu và số đơn trên tính trong cùng đơn vị thời gian với churn rate và AL ở trên (tính theo tháng).

$$
\text{Giá trị mang lại trung bình của 1 khách hàng} = \text{Giá trị trung bình của đơn hàng} x \text{Số đơn hàng trung bình của 1 khách}
$$

Cuối cùng, ta nhân giá trị trên với lifespan để ra LTV

$$
LTV = \text{Giá trị mang lại trung bình của 1 khách hàng} x \text{Vòng đời trung bình trên nền tảng của 1 khách hàng}
$$

Như vậy, ta đã tính được chi phí để có được 1 khách hàng CAC và giá trị trung bình 1 khách hàng mang lại LTV. Dễ thấy, ta muốn LTV càng cao càng tốt còn CAC thì ngược lại. Và tỷ lệ này **LTV/CAC** cũng là 1 chỉ số quan trọng để đánh giá khả năng tạo ra doanh thu của 1 nền tảng ecommerce, đó là `ROI`.

$$
ROI \text( Return on Investment) = \frac{LTV}{CAC} - 1
$$

____
Như vậy, mình đã đi qua các chỉ số mà mình nghĩ là quan trọng khi làm phân tích dữ liệu cho 1 nền tảng Ecommerce. Vì là những hiểu biết của bản thân còn hạn chế nên khó tránh khỏi những sai sót. Mong người đọc có thể đóng góp thêm để bài viết có thể được hoàn thiện hơn.

____
Tài liệu tham khảo:
1. Lean Analytics Book  
2. [How to deep dive in your product funnel performance with GA and Data Studio ](https://medium.com/@jspanom/how-to-deep-dive-in-your-product-funnel-performance-with-ga-and-data-studio-step-by-step-guide-328d1bbb4dd4)
3. [The Marketer’s Guide to Customer Acquisition Costs](https://medium.com/better-marketing/the-marketers-guide-to-customer-acquisition-costs-bf465b5903b0/)  
4. [The Marketer’s Guide to Customer Lifetime Value](https://medium.com/better-marketing/the-marketers-guide-to-customer-lifetime-value-7f0eb5991098/)  
5. [How to Calculate Customer Lifetime Value](https://blog.hubspot.com/service/how-to-calculate-customer-lifetime-value)