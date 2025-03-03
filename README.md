# bobby
trac nghiem cong nghe 
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Quiz: Động cơ đốt trong</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      background: #f9f9f9;
    }
    .quiz-container {
      max-width: 800px;
      margin: auto;
      padding: 20px;
      background: #fff;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      border-radius: 8px;
    }
    .quiz-container h1 {
      text-align: center;
    }
    .question {
      font-weight: bold;
      margin-top: 20px;
    }
    .options {
      list-style: none;
      padding: 0;
    }
    .options li {
      margin: 8px 0;
    }
    .btn {
      display: block;
      width: 100%;
      padding: 10px;
      margin-top: 20px;
      font-size: 16px;
      cursor: pointer;
      background: #4285f4;
      color: #fff;
      border: none;
      border-radius: 4px;
    }
    #result {
      margin-top: 20px;
      font-size: 18px;
      text-align: center;
      font-weight: bold;
      white-space: pre-line;
    }
    .review {
      margin-top: 20px;
    }
    .review .question-review {
      margin-bottom: 15px;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 4px;
    }
    .correct {
      color: green;
    }
    .incorrect {
      color: red;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>Quiz: Động cơ đốt trong</h1>
    <div id="quiz"></div>
    <button id="submit" class="btn">Nộp bài</button>
    <div id="result"></div>
    <div id="review" class="review"></div>
  </div>
  
  <script>
    const quizData = [
      // Câu 1 đến Câu 7
      { question: "Động cơ đốt trong là loại động cơ gì?", options: ["Động cơ điện", "Động cơ nhiệt", "Động cơ hơi nước", "Động cơ quang"], answer: "Động cơ nhiệt" },
      { question: "Chức năng chính của động cơ đốt trong là gì?", options: ["Tạo ra điện năng", "Biến đổi hóa năng thành nhiệt năng", "Biến đổi nhiệt năng thành công cơ học", "Sưởi ấm"], answer: "Biến đổi nhiệt năng thành công cơ học" },
      { question: "Động cơ đốt trong được sử dụng nhiều trong lĩnh vực nào?", options: ["Giao thông", "Xây dựng", "Nông nghiệp", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Động cơ đốt trong được phân loại theo tiêu chí nào?", options: ["Nhiên liệu sử dụng", "Chu trình công tác", "Phương pháp làm mát", "Tất cả các tiêu chí trên"], answer: "Tất cả các tiêu chí trên" },
      { question: "Động cơ sử dụng nhiên liệu nào không thuộc động cơ đốt trong?", options: ["Xăng", "Diesel", "Điện", "Gas"], answer: "Điện" },
      { question: "Chu trình làm việc của động cơ 4 kỳ gồm những kỳ nào?", options: ["Nạp, nén, nổ, xả", "Nạp, nén, cháy, xả", "Hút, nén, giãn nở, xả", "Hút, nén, nổ, thoát"], answer: "Nạp, nén, nổ, xả" },
      { question: "Động cơ diesel hoạt động theo nguyên lý nào?", options: ["Đánh lửa bằng bugi", "Nén hỗn hợp nhiên liệu - không khí đến nhiệt độ tự bốc cháy", "Dùng bộ chế hòa khí để trộn nhiên liệu", "Sử dụng pin nhiên liệu"], answer: "Nén hỗn hợp nhiên liệu - không khí đến nhiệt độ tự bốc cháy" },
      // Câu 8 đến Câu 14
      { question: "Động cơ hai kỳ và bốn kỳ được phân loại theo yếu tố nào?", options: ["Nhiên liệu sử dụng", "Chu trình công tác", "Số pít tông", "Số xylanh"], answer: "Chu trình công tác" },
      { question: "Động cơ chữ V được phân loại theo yếu tố nào?", options: ["Chu trình công tác", "Nhiên liệu sử dụng", "Cách bố trí xilanh", "Số xi lanh"], answer: "Cách bố trí xilanh" },
      { question: "Động cơ đốt trong biến đổi năng lượng dạng gì sang công cơ học?", options: ["Điện năng", "Hóa năng", "Công cơ học", "Nhiệt năng"], answer: "Hóa năng" },
      { question: "Động cơ đốt trong biến đổi nhiệt năng sang năng lượng dạng gì?", options: ["Điện năng", "Hóa năng", "Công cơ học", "Nhiệt năng"], answer: "Công cơ học" },
      { question: "Cơ cấu nào giúp tạo ra mô-men quay để dẫn động máy công tác?", options: ["Cơ cấu trục khuỷu – thanh truyền", "Cơ cấu phân phối khí", "Hệ thống nhiên liệu", "Hệ thống đánh lửa"], answer: "Cơ cấu trục khuỷu – thanh truyền" },
      { question: "Cơ cấu phân phối khí có nhiệm vụ gì?", options: ["Đóng mở cửa nạp, cửa thải đúng thời điểm", "Tạo mô-men quay đúng thời điểm", "Cung cấp nhiên liệu đúng thời điểm", "Làm mát động cơ đúng thời điểm"], answer: "Đóng mở cửa nạp, cửa thải đúng thời điểm" },
      { question: "Hệ thống nào giúp duy trì nhiệt độ của các chi tiết máy trong giới hạn nhất định?", options: ["Hệ thống nhiên liệu", "Hệ thống làm mát", "Hệ thống khởi động", "Hệ thống đánh lửa"], answer: "Hệ thống làm mát" },
      // Câu 15 đến Câu 17
      { question: "Hệ thống nào giúp động cơ bắt đầu làm việc?", options: ["Hệ thống khởi động", "Hệ thống đánh lửa", "Hệ thống phân phối khí", "Hệ thống làm mát"], answer: "Hệ thống khởi động" },
      { question: "Động cơ xăng có hệ thống nào mà động cơ Diesel không có?", options: ["Hệ thống nhiên liệu", "Hệ thống đánh lửa", "Hệ thống làm mát", "Hệ thống phân phối khí"], answer: "Hệ thống đánh lửa" },
      { question: "Động cơ Diesel sử dụng phương pháp nào để đốt cháy nhiên liệu?", options: ["Bugi đánh lửa đốt cháy Diesel", "Nén với áp suất và nhiệt độ cao, tự bốc cháy", "Phóng điện cao áp làm cháy Diesel", "Kim phun xăng vào buồng cháy"], answer: "Nén với áp suất và nhiệt độ cao, tự bốc cháy" },
      // Câu 18 đến Câu 21
      { question: "Ô tô, xe máy hiện đại thường được trang bị thêm hệ thống nào để giảm ô nhiễm?", options: ["Hệ thống làm mát", "Hệ thống xử lý khí thải", "Hệ thống bôi trơn", "Hệ thống nhiên liệu"], answer: "Hệ thống xử lý khí thải" },
      { question: "Động cơ nhiều xilanh có ưu điểm gì so với động cơ một xylanh?", options: ["Tạo công suất lớn hơn", "Hoạt động ổn định hơn", "Giảm rung lắc khi hoạt động", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Đâu là nơi lắp đặt, bố trí các cơ cấu và hệ thống của động cơ đốt trong?", options: ["Xilanh", "Thân máy, nắp máy", "Pít tông", "Các te."], answer: "Thân máy, nắp máy" },
      { question: "Động cơ đốt trong hoạt động dựa trên nguyên lý nào?", options: ["Đốt cháy nhiên liệu ngoài động cơ", "Đốt cháy nhiên liệu trong xylanh", "Dùng điện để làm quay động cơ", "Nén khí để sinh công"], answer: "Đốt cháy nhiên liệu trong xylanh" },
      // Câu 22 đến Câu 24
      { question: "Động cơ 4 kỳ có bao nhiêu hành trình piston trong một chu trình công tác?", options: ["1", "2", "3", "4"], answer: "4" },
      { question: "Trong các cách phân loại động cơ đốt trong sau, Cách phân loại nào dựa theo cách bố trí xilanh?", options: ["Động cơ xăng", "Động cơ 4 kì", "Động cơ chữ V", "Động cơ 2 kì"], answer: "Động cơ chữ V" },
      { question: "Một động cơ đốt trong có kí hiệu V8 là loại động cơ", options: ["có 8 xilanh", "có 8 xilanh bố trí thẳng hàng", "có 8 xilanh bố trí hình chữ V", "có 8 xilanh bố trí hình chữ A"], answer: "có 8 xilanh bố trí hình chữ V" },
      // Câu 25 đến Câu 27
      { question: "Vai trò của ô tô trong sản xuất là", options: ["nâng cao năng suất, chất lượng sản phẩm", "vận chuyển vật liệu, hàng hóa", "bảo vệ môi trường", "tiết kiệm tài nguyên thiên nhiên"], answer: "vận chuyển vật liệu, hàng hóa" },
      { question: "Ô tô có vai trò quan trọng trong đời sống vì", options: ["là phương tiện giao thông đi được trên nhiều địa hình khác nhau", "là phương tiện giao thông chở nhiều loại hàng hóa khác nhau", "là phương tiện giao thông chở được cả người và hàng hóa", "là phương tiện giao thông cơ động hơn tàu hỏa, tàu thủy, máy bay"], answer: "là phương tiện giao thông chở được cả người và hàng hóa" },
      { question: "Hệ thống truyền lực ô tô có nhiệm vụ", options: ["truyền mômen từ động cơ đến hộp số", "truyền và biến đổi mô men từ động cơ đến bánh xe chủ động", "tạo ra năng lượng để giúp ô tô chuyển động", "điều khiển hướng chuyển động của ô tô"], answer: "truyền và biến đổi mô men từ động cơ đến bánh xe chủ động" },
      // Câu 28 đến Câu 30
      { question: "Ở động cơ đốt trong dùng nhiên liệu xăng, quá trình đốt cháy hòa khí được thực hiện bằng cách", options: ["hòa khí trong xilanh tự động bốc cháy", "hòa khí trong xilanh được đốt cháy bằng tia lửa điện từ bugi", "hòa khí trong xilanh một phần tự bốc cháy, một phần được đốt cháy bằng tia lửa điện từ bugi", "hòa khí trong xilanh tự bốc cháy nhờ tiếp xúc với các chi tiết có nhiệt độ cao trong xilanh"], answer: "hòa khí trong xilanh được đốt cháy bằng tia lửa điện từ bugi" },
      { question: "Ở động cơ đốt trong dùng nhiên liệu Diesel, quá trình đốt cháy hòa khí được thực hiện bằng cách", options: ["hòa khí trong xilanh tự động bốc cháy", "hòa khí trong xilanh được đốt cháy bằng tia lửa điện từ bugi", "hòa khí trong xilanh một phần tự bốc cháy, một phần được đốt cháy bằng tia lửa điện từ bugi", "hòa khí trong xilanh tự bốc cháy nhờ tiếp xúc với các chi tiết có nhiệt độ cao trong xilanh"], answer: "hòa khí trong xilanh tự bốc cháy nhờ tiếp xúc với các chi tiết có nhiệt độ cao trong xilanh" },
      { question: "Phân loại theo chu trình công tác, động cơ đốt trong gồm:", options: ["Động cơ chữ V, động cơ thẳng hàng", "Động cơ chữ V, động cơ hình sao", "Động cơ xăng, động cơ Diesel", "Động cơ 2 kì, 4 kì"], answer: "Động cơ 2 kì, 4 kì" },
      // Câu 31 đến Câu 34
      { question: "Chu trình làm việc của động cơ 4 kì được mô tả gồm 4 quá trình theo thứ tự là", options: ["nạp, nén, nổ và cháy", "nạp, nén, giãn nở và thải", "nạp, nén, cháy – giãn nở và thải", "thải, nạp, nén, cháy - dãn nở"], answer: "nạp, nén, cháy – giãn nở và thải" },
      { question: "Điểm chết dưới là vị trí pít tông", options: ["xa tâm trục khuỷu nhất", "gần tâm trục khuỷu nhất", "xa đầu to thanh truyền nhất", "gần đầu to thanh truyền nhất"], answer: "xa tâm trục khuỷu nhất" },
      { question: "Điểm chết trên là vị trí pít tông", options: ["xa tâm trục khuỷu nhất", "gần tâm trục khuỷu nhất", "xa đầu to thanh truyền nhất", "gần đầu to thanh truyền nhất"], answer: "gần tâm trục khuỷu nhất" },
      { question: "Thể tích công tác của xi lanh động cơ đốt trong là thể tích", options: ["xilanh giới hạn bởi 2 điểm chết", "không gian giữa nắp xilanh, đỉnh pít tông khi pít tông ở điểm chết trên", "lớn nhất có thể của xilanh", "không gian giữa nắp xilanh, đỉnh pít tông khi pít tông đang ở điểm chết dưới"], answer: "xilanh giới hạn bởi 2 điểm chết" },
      // Câu 35 đến Câu 37
      { question: "Thể tích toàn phần của xi lanh động cơ đốt trong là thể tích", options: ["xilanh giới hạn bởi 2 điểm chết", "không gian giữa nắp xilanh, đỉnh pít tông khi pít tông ở điểm chết trên", "nhỏ nhất có thể của xilanh", "không gian giữa nắp xilanh, đỉnh pít tông khi pít tông ở điểm chết dưới"], answer: "không gian giữa nắp xilanh, đỉnh pít tông khi pít tông ở điểm chết trên" },
      { question: "Thể tích buồng cháy của xi lanh động cơ đốt trong là thể tích", options: ["xilanh giới hạn bởi 2 điểm chết", "không gian giữa nắp xilanh, đỉnh pít tông khi pít tông ở điểm chết trên", "lớn nhất có thể của xilanh", "không gian giữa nắp xilanh, đỉnh pít tông khi pít tông ở điểm chết dưới"], answer: "không gian giữa nắp xilanh, đỉnh pít tông khi pít tông ở điểm chết dưới" },
      // Câu 37 đến Câu 39
      { question: "Kí hiệu thể tích công tác là", options: ["Vh", "Vc", "Va", "Vb"], answer: "Vh" },
      { question: "Kí hiệu thể tích toàn phần là", options: ["Vh", "Vc", "Va", "Vb"], answer: "Va" },
      { question: "Kí hiệu thể tích buồng cháy là", options: ["Vh", "Vc", "Va", "Vb"], answer: "Vc" },
      // Câu 40
      { question: "Tỉ số nén là tỉ số giữa", options: ["Va/Vc", "Vc/Va", "Va/Vh", "Vh/Va"], answer: "Va/Vc" },
      // Câu 41 đến Câu 43
      { question: "1 chu trình làm việc của động cơ đốt trong được thực hiện trong 4 hành trình pít tông thì đây là động cơ mấy kì? (không học thuộc, chỉ nên học cách tính)", options: ["1", "2", "3", "4"], answer: "4" },
      { question: "Động cơ đốt trong 4 kì thực hiện 2 chu trình công tác thì pít tông đi được bao nhiêu hành trình? (không học thuộc, chỉ nên học cách tính)", options: ["2", "4", "6", "8"], answer: "8" },
      { question: "Chiếc xe Wave 110, số 110 nghĩa là", options: ["thể tích toàn phần", "thể tích công tác", "thể tích buồng cháy", "thể tích lớn nhất"], answer: "thể tích công tác" },
      // Câu 44 đến Câu 47
      { question: "Chiếc xe Dream 100, số 100 có là", options: ["thể tích công tác 100cc", "thể tích công tác 100 lít", "thể tích toàn phần 100 cm3", "thể tích buồng cháy 100 cc"], answer: "thể tích công tác 100cc" },
      { question: "Thể tích công tác càng lớn thì động cơ có", options: ["công suất càng lớn", "kích thước càng nhỏ", "công suất càng nhỏ", "số kì càng lớn"], answer: "công suất càng lớn" },
      { question: "Động cơ đốt trong 4 kì, 1 chu trình công tác thực hiện bởi bao nhiêu hành trình pít tông? (không học thuộc, chỉ nên học cách tính)", options: ["2", "4", "6", "8"], answer: "4" },
      { question: "Động cơ đốt trong 4 kì, 1 chu trình công tác thực hiện bởi bao nhiêu vòng quay trục khuỷu? (không học thuộc, chỉ nên học cách tính)", options: ["2", "4", "6", "8"], answer: "2" },
      // Câu 48 đến Câu 52
      { question: "Động cơ đốt trong 4 kì xăng khác Diesel ở chỗ nào?", options: ["Có bugi", "Có xupap", "Có pít tông", "Có vòi phun"], answer: "Có bugi" },
      { question: "Động cơ đốt trong 4 kì Diesel khác xăng ở chỗ nào?", options: ["Có bugi", "Có xupap", "Có pít tông", "Có vòi phun"], answer: "Có vòi phun" },
      { question: "ĐCĐT 4 kì Diesel, ở kì nạp, pít tông đi từ đâu đến đâu? (tương tự cho kì nén, cháy-giãn nở, thải)", options: ["ĐCT => ĐCD", "ĐCD => ĐCT", "Điểm chết nạp => điểm chết thải", "Điểm chết thải => điểm chết nạp"], answer: "ĐCT => ĐCD" },
      { question: "ĐCĐT 4 kì xăng, ở kì nạp, xupap nào mở, xupap nào đóng? (tương tự cho kì nén, cháy giãn nở, thải)", options: ["Xupap nạp mở, xupap thải đóng", "2 xupap mở", "2 xupap đóng", "Xupap nạp đóng, xupap thải mở"], answer: "Xupap nạp mở, xupap thải đóng" },
      { question: "ĐCĐT 4 kì xăng, kì nào là kì sinh công?", options: ["Kì nạp", "Kì nén", "Kì cháy – giãn nở", "Kì thải"], answer: "Kì cháy – giãn nở" },
      { question: "Ở kì nạp ĐCĐT 4 kì, thể tích xilanh (tương tự cho 3 kì còn lại)", options: ["giảm", "tăng", "không đổi", "tăng hoặc giảm đều đúng"], answer: "tăng" },
      { question: "Ở kì nạp ĐCĐT 4 kì, áp suất trong xilanh (tương tự cho kì nén, cháy giãn nở)", options: ["giảm", "tăng", "không đổi", "tăng hoặc giảm đều đúng"], answer: "giảm" },
      // Câu 53 đến Câu 54 đã được liệt kê ở trên

      // Từ Câu 55 đến Câu 98 (44 câu do tự tạo)
      { question: "Trong động cơ đốt trong, quá trình đốt cháy diễn ra chủ yếu ở phần nào của xi-lanh?", options: ["Phần trên của xi-lanh", "Phần dưới của xi-lanh", "Phần giữa của xi-lanh", "Toàn bộ xi-lanh"], answer: "Phần trên của xi-lanh" },
      { question: "Hệ thống bôi trơn trong động cơ đốt trong có vai trò gì?", options: ["Giảm ma sát giữa các bộ phận", "Làm mát động cơ", "Tăng công suất", "Điều chỉnh tốc độ động cơ"], answer: "Giảm ma sát giữa các bộ phận" },
      { question: "Bugi trong động cơ xăng có chức năng gì?", options: ["Phun nhiên liệu", "Đánh lửa", "Bôi trơn", "Làm mát"], answer: "Đánh lửa" },
      { question: "Trong động cơ Diesel, hệ thống phun nhiên liệu có tên gọi là gì?", options: ["Hệ thống phun xăng", "Hệ thống phun Diesel", "Hệ thống phun khí", "Hệ thống phun hỗn hợp"], answer: "Hệ thống phun Diesel" },
      { question: "Áp suất nén trong xi-lanh động cơ Diesel thường cao hơn so với động cơ xăng vì mục đích nào?", options: ["Để đánh lửa hỗn hợp", "Để tạo ra sự nén cao, giúp nhiên liệu tự bốc cháy", "Để tăng tốc độ động cơ", "Để giảm tiếng ồn"], answer: "Để tạo ra sự nén cao, giúp nhiên liệu tự bốc cháy" },
      { question: "Quá trình nén trong động cơ đốt trong có tác dụng gì?", options: ["Tăng nhiệt độ hỗn hợp khí", "Giảm áp suất", "Tăng lượng nhiên liệu", "Làm mát hỗn hợp khí"], answer: "Tăng nhiệt độ hỗn hợp khí" },
      { question: "Khi hoạt động, động cơ đốt trong cần được làm mát để tránh hiện tượng gì?", options: ["Quá nhiệt", "Quá lạnh", "Độ ẩm cao", "Độ ồn lớn"], answer: "Quá nhiệt" },
      { question: "Hệ thống làm mát của động cơ thường sử dụng chất lỏng nào?", options: ["Nước", "Dầu nhớt", "Không khí", "Xăng"], answer: "Nước" },
      { question: "Trong động cơ, bộ giảm chấn có vai trò gì?", options: ["Giảm rung động", "Tăng công suất", "Tăng nhiệt độ", "Giảm ma sát"], answer: "Giảm rung động" },
      { question: "Khi động cơ chạy ở tốc độ cao, yếu tố nào quan trọng nhất để bảo vệ động cơ?", options: ["Hệ thống đánh lửa", "Hệ thống làm mát", "Hệ thống phun nhiên liệu", "Hệ thống bôi trơn"], answer: "Hệ thống làm mát" },
      { question: "Động cơ đốt trong thường được làm mát bằng hệ thống nước, đúng hay sai?", options: ["Đúng", "Sai", "Chỉ khi trời nóng", "Chỉ khi động cơ chạy ở tốc độ thấp"], answer: "Đúng" },
      { question: "Trong quá trình đốt cháy, khi nhiệt độ tăng đột biến, điều gì xảy ra?", options: ["Sự bốc cháy nhanh hơn", "Sự bốc cháy chậm lại", "Không có gì thay đổi", "Động cơ dừng lại ngay lập tức"], answer: "Sự bốc cháy nhanh hơn" },
      { question: "Tỉ số nén cao trong động cơ thường dẫn đến:", options: ["Tăng hiệu suất nhiệt", "Giảm hiệu suất nhiệt", "Tăng tiêu hao nhiên liệu", "Giảm công suất động cơ"], answer: "Tăng hiệu suất nhiệt" },
      { question: "Một động cơ đốt trong hiệu quả thường có tỉ số nén trong khoảng:", options: ["8:1 đến 10:1", "10:1 đến 12:1", "12:1 đến 15:1", "15:1 đến 20:1"], answer: "10:1 đến 12:1" },
      { question: "Phần nào của động cơ chịu tác động lớn nhất từ quá trình nén và cháy?", options: ["Xi-lanh", "Pít tông", "Trục khuỷu", "Cờ lê"], answer: "Pít tông" },
      { question: "Trong động cơ, sự chậm trễ của hệ thống đánh lửa có thể gây ra:", options: ["Tăng công suất", "Giảm hiệu suất và rung động", "Tiết kiệm nhiên liệu", "Tăng tuổi thọ động cơ"], answer: "Giảm hiệu suất và rung động" },
      { question: "Một số động cơ hiện đại sử dụng công nghệ 'phun trực tiếp' nhằm mục đích nào?", options: ["Tăng hiệu suất đốt cháy", "Giảm khí thải", "Tiết kiệm nhiên liệu", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Việc duy trì áp suất ổn định trong buồng đốt là quan trọng vì:", options: ["Giúp động cơ khởi động", "Tăng hiệu suất đốt cháy", "Giảm tiếng ồn", "Giảm tiêu hao dầu nhớt"], answer: "Tăng hiệu suất đốt cháy" },
      { question: "Trong động cơ đốt trong, quá trình giãn nở diễn ra sau quá trình nào?", options: ["Sau nạp", "Sau nén", "Sau cháy", "Sau xả"], answer: "Sau cháy" },
      { question: "Một hệ thống làm mát hiệu quả giúp động cơ hoạt động ổn định, đúng hay sai?", options: ["Đúng", "Sai"], answer: "Đúng" },
      { question: "Hệ thống bôi trơn trong động cơ thường dùng dầu nhớt, đúng hay sai?", options: ["Đúng", "Sai"], answer: "Đúng" },
      { question: "Khi động cơ chạy ở tốc độ thấp, hiệu suất đốt cháy thường:", options: ["Tăng", "Giảm", "Không thay đổi", "Biến động không ổn định"], answer: "Giảm" },
      { question: "Động cơ xăng và động cơ Diesel khác nhau chủ yếu ở:", options: ["Hệ thống đánh lửa", "Hệ thống phun nhiên liệu", "Tỉ số nén", "Cả ba yếu tố trên"], answer: "Cả ba yếu tố trên" },
      { question: "Trong động cơ xăng, bugi có vai trò quan trọng trong việc:", options: ["Đánh lửa hỗn hợp khí-nhiên liệu", "Phun nhiên liệu", "Hỗ trợ làm mát", "Bảo vệ piston"], answer: "Đánh lửa hỗn hợp khí-nhiên liệu" },
      { question: "Hệ thống điều khiển động cơ hiện đại thường sử dụng bộ vi xử lý để:", options: ["Kiểm soát lượng nhiên liệu phun vào", "Điều chỉnh thời gian đánh lửa", "Giám sát hoạt động của động cơ", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Động cơ đốt trong có thể được cải tiến bằng công nghệ nào để giảm khí thải?", options: ["Sử dụng chất xúc tác", "Tăng tỉ số nén", "Giảm kích thước piston", "Thay đổi loại nhiên liệu"], answer: "Sử dụng chất xúc tác" },
      { question: "Một động cơ có hiệu suất cao thường cho thấy:", options: ["Tiêu hao nhiên liệu thấp", "Tiêu hao nhiên liệu cao", "Không tiêu hao nhiên liệu", "Tiêu hao dầu nhớt nhiều"], answer: "Tiêu hao nhiên liệu thấp" },
      { question: "Các yếu tố nào ảnh hưởng đến hiệu suất của động cơ đốt trong?", options: ["Tỉ số nén", "Thời gian đánh lửa", "Hệ thống phun nhiên liệu", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Mức độ nén quá cao trong động cơ có thể dẫn đến:", options: ["Hiệu suất tăng", "Gây hư hỏng động cơ", "Tiết kiệm nhiên liệu", "Hoạt động êm ái hơn"], answer: "Gây hư hỏng động cơ" },
      { question: "Trong quá trình thiết kế, việc mô phỏng đốt cháy hỗn hợp trong xi-lanh giúp:", options: ["Dự đoán hiệu suất động cơ", "Tối ưu hóa thời gian đánh lửa", "Giảm chi phí sản xuất", "Tăng kích thước động cơ"], answer: "Dự đoán hiệu suất động cơ" },
      { question: "Một động cơ đốt trong hoạt động hiệu quả khi các bộ phận được thiết kế để:", options: ["Tối ưu hóa sự trao đổi nhiệt", "Tăng kích thước xi-lanh", "Giảm trọng lượng xe", "Tăng tốc độ quay của trục khuỷu"], answer: "Tối ưu hóa sự trao đổi nhiệt" },
      { question: "Tốc độ động cơ thường được đo bằng đơn vị nào?", options: ["Vòng/phút", "Mét/giây", "Kilowatt", "Mile/giờ"], answer: "Vòng/phút" },
      { question: "Động cơ đốt trong xăng thường có chu trình làm việc là:", options: ["Hai kỳ", "Bốn kỳ", "Sáu kỳ", "Tám kỳ"], answer: "Bốn kỳ" },
      { question: "Hệ thống làm mát đóng vai trò quan trọng trong việc:", options: ["Giảm tiêu hao nhiên liệu", "Bảo vệ động cơ khỏi quá nhiệt", "Tăng tốc độ động cơ", "Tăng công suất động cơ"], answer: "Bảo vệ động cơ khỏi quá nhiệt" },
      { question: "Trong động cơ Diesel, áp suất nén cao giúp:", options: ["Giảm tiêu hao nhiên liệu", "Tăng nhiệt độ hỗn hợp", "Kích hoạt quá trình tự bốc cháy", "Cả B và C"], answer: "Cả B và C" },
      { question: "Một động cơ đốt trong hiệu quả cần có:", options: ["Hệ thống đánh lửa chính xác", "Hệ thống phun nhiên liệu tối ưu", "Hệ thống làm mát hiệu quả", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Hệ thống cảm biến trong động cơ đốt trong thường giám sát:", options: ["Nhiệt độ", "Áp suất", "Lượng khí thải", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Động cơ đốt trong được thiết kế để hoạt động liên tục với mục đích:", options: ["Tăng công suất đột ngột", "Hoạt động ổn định và bền bỉ", "Giảm tiếng ồn", "Tiết kiệm nhiên liệu"], answer: "Hoạt động ổn định và bền bỉ" },
      { question: "Trong động cơ đốt trong, việc duy trì tỉ lệ không khí - nhiên liệu đúng là:", options: ["Quan trọng để đạt hiệu suất tối ưu", "Không quan trọng lắm", "Chỉ cần khi động cơ mới", "Chỉ cần khi bảo dưỡng"], answer: "Quan trọng để đạt hiệu suất tối ưu" },
      { question: "Một số động cơ hiện đại sử dụng công nghệ biến thiên van nhằm mục đích:", options: ["Tối ưu hóa hiệu suất", "Giảm khí thải", "Tăng công suất", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Động cơ đốt trong có thể sử dụng các loại nhiên liệu khác nhau, ví dụ:", options: ["Xăng, Diesel", "Gas tự nhiên, LPG", "Ethanol", "Tất cả các đáp án trên"], answer: "Tất cả các đáp án trên" },
      { question: "Trong thiết kế động cơ, việc giảm ma sát giữa các bộ phận chủ yếu được thực hiện qua:", options: ["Sử dụng vật liệu bôi trơn", "Tăng kích thước piston", "Giảm tỉ số nén", "Thay đổi thiết kế van"], answer: "Sử dụng vật liệu bôi trơn" },
      { question: "Động cơ đốt trong có thể hoạt động với các chu trình khác nhau, nhưng phổ biến nhất là chu trình:", options: ["Hai kỳ", "Bốn kỳ", "Sáu kỳ", "Tám kỳ"], answer: "Bốn kỳ" },
      { question: "Mục tiêu chính của việc phát triển công nghệ động cơ đốt trong là:", options: ["Tăng công suất", "Giảm khí thải và tiêu hao nhiên liệu", "Tăng tuổi thọ động cơ", "Tất cả các đáp án trên"], answer: "Giảm khí thải và tiêu hao nhiên liệu" }
      // Tổng cộng 98 câu hỏi
    ];
    
    const quizContainer = document.getElementById("quiz");
    const submitButton = document.getElementById("submit");
    const resultContainer = document.getElementById("result");
    const reviewContainer = document.getElementById("review");
    
    function loadQuiz() {
      quizData.forEach((currentQuestion, questionIndex) => {
        const questionDiv = document.createElement("div");
        questionDiv.classList.add("question");
        questionDiv.innerText = (questionIndex + 1) + ". " + currentQuestion.question;
        quizContainer.appendChild(questionDiv);
        
        const optionsList = document.createElement("ul");
        optionsList.classList.add("options");
        currentQuestion.options.forEach(option => {
          const optionItem = document.createElement("li");
          const radioInput = document.createElement("input");
          radioInput.type = "radio";
          radioInput.name = "question" + questionIndex;
          radioInput.value = option;
          const label = document.createElement("label");
          label.innerText = option;
          optionItem.appendChild(radioInput);
          optionItem.appendChild(label);
          optionsList.appendChild(optionItem);
        });
        quizContainer.appendChild(optionsList);
      });
    }
    
    function showResults() {
      let score = 0;
      reviewContainer.innerHTML = "";
      
      quizData.forEach((currentQuestion, questionIndex) => {
        const selectedOption = document.querySelector('input[name="question' + questionIndex + '"]:checked');
        const userAnswer = selectedOption ? selectedOption.value : "Không trả lời";
        const isCorrect = (userAnswer === currentQuestion.answer);
        if (isCorrect) {
          score++;
        } else {
          const reviewDiv = document.createElement("div");
          reviewDiv.classList.add("question-review");
          reviewDiv.innerHTML = `<strong>Câu ${questionIndex + 1}:</strong> ${currentQuestion.question}<br>
            <span>Your answer: <em class="incorrect">${userAnswer}</em></span><br>
            <span>Correct answer: <em class="correct">${currentQuestion.answer}</em></span>`;
          reviewContainer.appendChild(reviewDiv);
        }
      });
      
      resultContainer.innerText = "Bạn trả lời đúng " + score + " / " + quizData.length + " câu.\n" +
                                  "Các câu sai được hiển thị bên dưới:";
    }
    
    submitButton.addEventListener("click", () => {
      showResults();
    });
    
    loadQuiz();
  </script>
</body>
</html>
