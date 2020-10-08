---
layout: post
title: (Hầu như) Tất cả những thứ bạn cần biết về A/B Testing 
subtitle: Xác suất thống kê ứng dụng vào sản phẩm kinh doanh của bạn như nào
tags: [data, a/b testing]
comments: true
bigimg: /img/abtesting/bg.jpeg
banner: /img/abtesting/banner.png
img1: /img/abtesting/lazada.png
plot1: /img/abtesting/plot1.png
thumbnail: https://pakota159.github.io/img/abtesting/bg.jpeg
---

### Đối tượng và giới hạn bài viết

Nhờ các góp ý từ bài viết trước, trong bài này mình muốn đề cập đến đối tượng và giới hạn nội dung của bài viết này:

- Bài viết chủ yếu dành cho những người đã có kiến thức cơ bản về xác suất thống kê ví dụ kiến thức về kỳ vọng, phương sai, độ lệch chuẩn, biến xác suất ngẫu nhiên, phân phối mật độ xác suất, định lý giới hạn trung tâm, ...
- Tập trung vào ứng dụng A/B Testing trong UI/UX, mặc dù A/B Testing có thể được dùng cho những mảng khác, nhưng ở đây mình chỉ ví dụ trong UI/UX, các bạn có thể tự suy ra phương pháp trong những lĩnh vực khác.
- Nội dung được viết dựa trên `kiến thức và kinh nghiệm của bản thân mình`, nên `có thể đúng hoặc sai` và `chỉ mang tính tham khảo`. Nếu các bạn thấy có chỗ nào mình viết chưa hợp lý, không chính xác thì hãy bình luận ở cuối bài nhé. Mình cảm ơn.

________

Khi bắt đầu viết bài này, mình mới tìm hiểu lại kỹ về những yếu tố toán học phía sau 
________

### Phân tích bài toán

Giả sử, bạn đang là cô-founder (hoặc chú-founder) của 1 start-up nào đó. Sản phẩm của bạn tốt nhưng bạn muốn cải thiện UI-UX của nó để nó có thể tốt hơn.

Muốn làm cho sản phẩm tốt hơn, thì bạn phải biết nó đang `không tốt` ở chỗ nào đã.    

Để cho cụ thể, mình sẽ thử phân tích 1 phần UI/UX trang homepage của Lazada. Các phân tích phía sau đều là *giả thuyết* và *mang tính minh hoạ* cho ý tưởng.

#### 1. Từ dữ liệu xác định chỉ số cần cải thiện (xác định mục tiêu)

Trong trang homepage có rất nhiều phần/section khác nhau, và mình sẽ thử tính toán số liệu ở section đầu tiên - cái **banner ở homepage** này.

![banner]({{ page.banner }}#banner)

Giả sử, bạn vào trong data warehouse của công ty và query ra 2 thông số là **lượt view banner** và **lượt click banner**.

| section | view_count | click_count | click_rate (click_count / view_count)|
| ------- |--------| ------ | ------ |
| banner | 150,000 | 750 | 0.5% |

Tất nhiên, số kia mình bịa ra nên nó hơi cực đoan 1 chút, ta biết `CTR của 1 banner quảng cáo dạng slider là khoảng 1%` (mình lấy số từ 1 nghiên cứu của đại học Notre Dame [Link tại đây](https://erikrunyon.com/2013/07/carousel-interaction-stats/), số này cũng chỉ mang tính tham khảo vì mình không biết số phù hợp trong trường hợp này), 

Vì vậy, tỷ lệ click `0.5%` ở trên là thấp và do đó **mục tiêu là cần tìm cách sửa banner để cải thiện click rate của banner.**


#### 2. Dựa vào kinh nghiệm cá nhân hoặc Heuristic Evaluation để xác định vấn đề
Giờ thì ta cần phân tích xem cái banner đang có vấn đề gì.

Theo mình thì banner đã được `thiết kế đẹp`, `màu sắc hài hoà`, `nội dung liên quan đến dịp trung thu` sắp tới, `khuyến mãi cũng rõ ràng`, tuy nhiên có 1 phần mà tớ cảm thấy hơi có vấn đề là nút CTA (Call-to-Action) `Mua Ngay`.

Liệu nút CTA có nên đặt ở phần giữa phía dưới (`bottom-center`) của banner sẽ ổn hơn; hay là ngay dưới dòng khuyến mãi `Sắp sửa chơi trăng` (`bottom-left`) và chuyển cái hashtag sang bên phải vì mình cảm thấy người dùng sẽ dễ click vào CTA hơn nếu nó ở giữa hoặc ở ngay phía bên trái (do mắt người sẽ đọc từ trái sang phải); hoặc là chả cần cái nút này nữa. 

![img1]({{ page.img1 }}#img1)

Sau tất cả, đó chỉ là suy đoán **cảm tính** của mình, và mình cần 1 căn cứ đáng tin cậy hơn để quyết định vị trí đặt CTA.

#### 2. Thử nghiệm

Như vậy, mình đã đưa ra 1 số *phán đoán* và giờ mình cần thử nghiệm để xem phán đoán nào chính xác. Mình sẽ thử nghiệm với 2 vị trí CTA là `bottom-left` và `bottom-right` (những giải pháp khác cũng làm tương tự). 

Mình chọn mẫu người dùng với số lượng 10,000 người dùng cho mỗi vị trí. Nhóm A là 10,000 người dùng ngẫu nhiên và banner homepage mà những người này nhìn thấy sẽ là CTA đặt ở `bottom-right`; nhóm B cũng là 10,000 người ngẫu nhiên (tất nhiên khác với 10,000 người nhóm A) sẽ nhìn thấy CTA đặt ở `bottom-left`.

Và ta cần xác định CTR của phương án nào tốt hơn, hay là vị trí đặt nút `Mua Ngay` hoàn toàn không ảnh hưởng gì đến CTR.

|| A (bottom-right) | B (bottom-left) | 
|-----| ------- |--------| ------ | ------ |
|Number of users | 10,000  | 10,000  |
|CTR (Click through rate) | ?? | ?? |


#### 3. Thu thập dữ liệu và phân tích

Mình chạy thí nghiệm kia trong khoảng 1 tháng và thu thập được dữ liệu .

Để ví dụ, thì mình sẽ dùng R để fake số.

```r
# nhóm A có 30 bản ghi, giá trị mean là 0.415 và sd là 0.05, phân phối chuẩn
a_group = rnorm(30, mean=0.415, sd=0.05)

# nhóm B cũng có 30 bản ghi, giá trị mean là 0.45 và sd là 0.1, phân phối chuẩn
b_group = rnorm(30, mean=0.45, sd=0.1)
```

Giá trị trong 2 vectors trên có thể biểu diễn như ở bảng dưới.

|Date|CTR from A (bottom-right) | CTR from B (bottom-left) | 
|-----| ------- |--------|
|1/8/2020 | 0.493  | 0.262  |
|2/8/2020 | 0.428 | 0.408 |
|3/8/2020 | 0.463 | 0.35 |
|...|...|...|
|29/8/2020 | 0.452 | 0.326 |
|30/8/2020 | 0.389 | 0.458 |

Để dễ hình dung ra dữ liệu này nó như thế nào, chúng ta sẽ `visualize` nó.

```r
barplot(cbind(a_group, b_group), beside=TRUE)
```

![plot1]({{ page.plot1 }}#plot1)

Có thể thấy, ngay từ việc "tạo" dữ liệu và đồ thị thì CTR của nhóm A phân tán ít hơn nhóm B (sd nhỏ hơn), nhưng giá trị trung bình cũng nhỏ hơn. Câu hỏi lúc này là dựa vào dữ liệu như trên thì có thể kết luận `CTR trung bình của nhóm B tốt hơn của A không`.

Bài toán được quy về câu hỏi `hypothesis testing` trong thống kê:

**Welch’s t-test để kiểm định 2 kỳ vọng $$\mu_1$$, $$\mu_2$$**, ở đây 2 mẫu t-test là a_group và b_group và giả thuyết phương sai 2 mẫu này giống nhau là hợp lý vì 




________
Tham khảo:
1. Một bài viết hay về Banner trên website: [Do you really need carousel banner](https://medium.com/imagine-ux/do-you-really-need-carousel-banner-offers-running-on-your-homepage-19adf28d2a62)

2. Khoá học cơ bản về xác suất thống kê hay nhất mình từng đọc, it's just too good to be true: [Introduction to Probability and Statistics - MIT](https://ocw.mit.edu/courses/mathematics/18-05-introduction-to-probability-and-statistics-spring-2014/)

3. Khoá học Statistical Reasoning của Johns Hopkins School [Link here](http://ocw.jhsph.edu/index.cfm/go/viewCourse/course/StatisticalReasoning1/coursePage/index/)

4. A/B Testing from lecture of Data 8 course UC Berkeley [Lecture 19 - Data 8 course](http://data8.org/materials-sp18/lec/lec19PDF.pdf)

5. 1 công cụ thú vị của Evan Miller về A/B testing: [Simulation](https://www.evanmiller.org/ab-testing/t-test.html#!58.175/28.017074/8;33.71/11.841026/10@95)