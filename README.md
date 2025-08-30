# chienql.github.io
Tổng quan về giấu tin trong ảnh
Giấu tin là một kỹ thuật nhằm che giấu dữ liệu bí mật trong một đối tượng số như các file video, ảnh, âm thanh, cơ sở dữ liệu, chuỗi DNA, văn bản,… Mục đích chính của giấu tin là để người khác không thể nhận biết, tính mạnh mẽ, lượng tin che giấu trong đối tượng số. Bài báo này tổng hợp các kỹ thuật giấu tin trong ảnh số cũng như một số khái niệm cơ bản trong lĩnh vực bảo mật, an toàn dữ liệu thông qua che giấu dữ liệu.  Một số phương pháp che giấu dữ liệu trong định dạng JPEG cũng được thảo luận trong bài viết này. Có ba kỹ thuật liên quan với nhau là steganography (giấu tin), watermarking (thủy vân) và cryptography (mã hóa). Kỹ thuật giấu tin đề cập đến việc che giấu dữ liệu mà không nhận ra bằng mắt thường, kỹ thuật thủy vân có thể nhúng dữ liệu vào một vùng nào đó trên đối tượng và có thể nhận biết bằng mắt thường. Một ví dụ điển hình của thủy vân số là một video trên các kênh truyền hình có gắn biểu tượng của đài truyền hình. Nghiên cứu này sẽ mô tả các kỹ thuật giấu ảnh, sau đó so sánh các kỹ thuật dựa trên các đặc điểm khác nhau.  <img width="468" height="158" alt="image" src="https://github.com/user-attachments/assets/a44c97a7-fc36-4cc3-9bfb-f7f06e90af8a" />

1. Introduction
Thuật ngữ Steganography được dịch tử tiếng Hy Lạp với nghĩa là “Covered Writing”, là nghệ thuật ẩn dữ liệu vào một đối tượng. It has been used in different forms for thousands of years. Quá trình che giấu dữ liệu trong các dữ liệu số với nhiều phương pháp khác nhau, song hầu hết thực hiện bằng việc thay thế các bits dữ liệu sao cho sự thay đổi là nhỏ nhất để mắt thường không thể nhìn thấy. Tuy nhiên, quá trình này đòi hỏi xem xét đến ba yếu tố chính, đó là, dung lượng dữ liệu được nhúng vào đối tượng, bảo mật giúp cho việc chống đỡ của đối tượng và dữ liệu trước sự tấn công từ bên ngoài, và đặc biệt là tránh cho người khác có thể phát hiện [1, 2]. Qua các giai đoạn lịch sử phát triển của giấu tin, chúng ta có thể nhận thấy, trong những thế kỷ trước đó đã có những tác phẩm nghệ thuật của danh họa Picasso đã che giấu thông điệp vào các tác phẩm của ông, và đến ngày nay, khi công nghệ kỹ thuật số phát triển, các dữ liệu số được biểu diễn bằng các bit nhị phân dẫn đến việc che giấu thông tin thuận tiện hơn [3, 4]. Ba hình thức che giấu dữ liệu phổ biến ngày nay bao gồm giấu tin, thủy vân và mật mã học (Hình 1). 
Giấu tin nhằm mục đích che giấu dữ liệu bí mật vào một đối tượng với mục đích không để cho người khác phát hiện ra. Việc này đòi hỏi đối tượng chứa có thể gần như không hề bị thay đổi, hoặc nếu có thì sự thay đổi đó là rất nhỏ. Ví dụ, khi chúng ta giấu một số bits dữ liệu vào một file văn bản thì có thể thực hiện bằng việc chèn thêm kí tự trắng (dấu cách) vào sau dấu chấm của đoạn văn bản để với mắt thường sẽ không phát hiện ra sự thay đổi này.

Hình 1: Phân cấp hệ thống bảo mật

Kỹ thuật thứ hai là thủy vân, trong các tài liệu thường dịch sang là thủy vân số, vì môi trường nhúng dữ liệu ẩn là môi trường số. Thủy vân số đề cập đến việc nhúng một thành phần nào đó vào một đối tượng khác bằng việc in dấu vết lên đối tượng. Tùy thuộc vào việc chúng ta có cần cho người khác biết được thành phần được nhúng thể hiện trên đối tượng hay không. Ví dụ, danh họa thiết kế ra một bức ảnh số, họ có thể cho người khác biết đó là bức ảnh của mình thì danh họa sẽ thực hiện bằng việc in chữ kí lên đó. Một ví dụ khác, các chương trình của đài truyền hình hay các video của một tổ chức nào đó muốn cho người khác biết đó là sản phẩm của tổ chức mình thì thường họ nhúng logo của tổ chức lên video hoặc chương trình truyền hình. Những hình thức như trên được gọi là kỹ thuật Visible wartermarking. Ngược lại, một số tác giả chỉ muốn đánh dấu tác phẩm của mình bằng việc ghi mờ thông tin về tác giả để tác phẩm của họ không bị pha tạp thì họ có thể đánh dấu mờ mà mắt thường không phát hiện ra, song nếu có sự tranh chấp thì họ có thể chứng minh bằng cách trích xuất thông tin trong tác phẩm để khẳng định bản quyền của họ [5]. 
Khác với hai kỹ thuật trên, mã hóa được thực hiện bằng cách thay thế hoàn toàn dữ liệu ban đầu bằng một dữ liệu mà người khác không thể suy luận ra được. Ví dụ, đoạn văn bản DHSPKTHY sẽ được thay thế bằng WQTEFYQX, không có ý nghĩa. Có nhiều phương pháp để thực hiện mã hóa, trong đó có mã hóa dòng và mã hóa khối. Mã hóa dòng được thực hiện bằng cách thay thế tương ứng một kí tự này bằng một kí tự khác bằng một hình thức nào đó. Mã hóa khối được thực hiện bằng việc chi dữ liệu ra thành từng khối với kích thước nhất định (ví dụ, 64bits, tương ứng với 8 kí tự một khối), sau đó sử dụng một thuật toán phức tạp để sinh ra một khối dữ liệu khác. [6]. Với kỹ thuật này, để biết được dữ liệu gốc, người ta có thể thực hiện bằng các phương pháp thám mã, nghĩa là, họ sẽ tìm cách để biết được thuật toán và khóa sử dụng để mã hóa. Hình 1 thể hiện việc phân loại các kỹ thuật che giấu dữ liệu. 
Để tìm hiểu thêm về các kỹ thuật này, phần nội dung tiếp theo chúng tôi sẽ trình bày chi tiết hơn về các thuật toán giấu tin. 
	Các đặc tính của kỹ thuật giấu tin
	Sự an toàn
Kỹ thuật giấu tin có thể bị ảnh hưởng từ nhiều sự tấn công chủ động và thụ động  khác nhau.  Do đó, việc che giấu dữ liệu cần tính toán đến sự an toàn của dữ liệu ẩn. Liên quan đến vấn đề này, các thuật toán giấu tin cần phải quan tâm đến các hệ thống phân tích ẩn. Nếu sự tồn tại của thông tin mật có xác suất không cao hơn sự dự đoán ngẫu nhiên của các hệ thống phân tích ẩn thì thuật toán giấu tin là an toàn, nghĩa là có thể không bị phát hiện ra.  
	Dung lượng tin được che giấu
Dung lượng tin là kích thước của dữ liệu mà có thể được che giấu và có liên quan đến kích thước của đối tượng dùng để giấu tin. Nếu kích thước của đối tượng nhỏ thì lượng tin có thể nhúng vào rất ít. Ví dụ, một byte của đối tượng chỉ có thể nhúng 1 bit của dữ liệu mật thì với một bức ảnh màu có kích thước 1280 x 768 thì chúng ta có thể nhúng khoảng 61KB tài liệu mật. Ngược lại, với ảnh màu 8K với kích thước 7680 x 4320 thì dung lượng nhúng vào có thể lên tới 2MB dữ liệu. Do vậy, trước khi giấu tin vào đối tượng nào đó, thông thường, người ta phải tính toán xem kích thước của đối tượng có đủ để che giấu dữ liệu của mình hay không.  
	Độ trong suốt
Khi che giấu dữ liệu, có thể sẽ làm vật chứa bị biến dạng. Do đó, khi che giấu thông tin vào vật thể, cần phải sử dụng phương pháp tối ưu nhất để lượng tin giấu tăng lên đáng kể, trong khi vẫn giữ được tính trong suốt của đối tượng. Ví dụ, sau khi nhúng dữ liệu vào một bức ảnh, nếu để bản gốc của  bức ảnh và bản chứa dữ liệu ẩn cạnh nhau mà không phát hiện thấy sự khác biệt nào thì ta nói rằng độ trong suốt của thuật toán giấu tin là khá tốt. 
	Tính mạnh mẽ
Tính mạnh mẽ là một tiêu chí quan trọng trong các thuật toán giấu tin. Tiêu chí này đề cập đến mức độ khó khăn mà các phương pháp phân tích ẩn có thể xác định được đối tượng đang chứa dữ liệu ẩn hay không. Tính mạnh mẽ thường được sử dụng trong các phương pháp bảo vệ quyền tác giả [7].
	Các ứng dụng của kỹ thuật giấu tin
Có rất nhiều ứng dụng giấu tin trong ảnh bao gồm cả việc truyền tin mật, và bảo vệ quyền tác giả [8]. 
	Truyền tin mật
Trong nhiều trường hợp, việc truyền tin mật thu hút sự chú ý không mong muốn. Do vậy, để tránh sự chú ý của người khác, chúng ta cần phải nhúng thông điệp mật này vào một đối tượng hoặc có thể sử dụng các kỹ thuật như chia sẻ mã bí mật. Phương pháp chia sẻ mã bí mật thường được thực hiện bằng cách tạo sự nhiễu loạn của bản gốc trong n bản sao chép, người gửi và người nhận quy định số bản tối thiểu ghép lại (k bản) với nhau để tái tạo bản gốc. Bằng cách thức này, dữ liệu mật cũng sẽ được đảm bảo ngay cả khi kẻ tấn công sử dụng kỹ thuật Man-In-The-Middle [SS1]. 
	Bảo vệ quyền tác giả
Trong thủy vân số (watermarking), thông tin bản quyền bí mật có thể được nhúng vào ảnh để xác định đó là sản phẩm trí tuệ [5, 7]. Thủy vân số được thực hiện bằng cách kiểm tra thống kê, tính tương quan, tương đồng hoặc đo các đặc điểm số lượng khác trong hình ảnh ẩn. Việc chèn và phân tích tủy vân nhằm bảo vệ tài liệu có bản quyền khiến sự quan tâm của các nhà khoa học đến lĩnh vực này ngày càng tăng cao. 
	Nhận dạng thông minh
Trong nhận dạng thông minh, thông tin của một cá nhân được nhúng vào ảnh của họ nhằm bảo mật thông tin và ngăn ngừa tội phạm [10]. Để thực hiện được nhiệm vụ này, đòi hỏi người thực hiện hiểu và thực hiện được các kỹ thuật giấu tin trong ảnh.  
	Máy in
Một số máy in màu hiện đại như HP sử dụng kỹ thuật giấu tin để nhúng thông tin bí mật của nhà sản xuất. Trong các máy in này, các chấm màu vàng rất nhỏ được in lên tất cả các trang. Các thông tin về ngày, giờ, số Seri được ẩn trong các chấm màu vàng này [11].
	Phương pháp giấu tin trong ảnh
 Giấu tin trong ảnh số [12, 13] chủ yếu tập trung vào việc che giấu dữ liệu vào ảnh đa mức xám hoặc ảnh màu. Độ sáng của ảnh xám và ảnh màu gần như tương đương, vì vậy, một số nghiên cứu cho rằng việc giấu tin trong ảnh màu có khả năng dễ bị phát hiện hơn so với ảnh xám [14]. Trong phần này, chúng ta sẽ tìm hiểu các phương pháp giấu tin trong các bức ảnh số. 
	Các phương pháp giấu tin trong miền không gian
Đặc điểm chung của các phương pháp giấu tin trong miền không gian là thay đổi giá trị của các điểm ảnh. Tốc độ nhúng dữ liệu thường được đo bằng bpp (bit per pixel). Ví dụ, với phương pháp giấu tin trong bit có trọng số nhỏ nhất (LSB - Least Significant Bit) với một điểm ảnh màu có 4 Byte thì tốc độ nhúng sẽ là 4bpp. Phương pháp giấu tin trong bit LSB thường là đơn giản, song nó cũng có tác động lớn hơn so với các phương pháp khác [15]. 
Giấu tin dựa trên bit có trọng số nhỏ nhất (LSB)
Trong phương pháp giấu dựa trên LSB, mỗi điểm ảnh (pixel) của ảnh chứa được thay thế bằng giá trị của các bit dữ liệu ẩn tương ứng. Để lựa chọn điểm ảnh của ảnh chứa có thể được xác định bằng một khóa bí mật. Định dạng ảnh thường sử dụng trong phương pháp này là ảnh Bitmap (BMP) 24bits, vì kích thước ảnh thường rất lớn. Một số nghiên cứu cũng đã sử dụng phương pháp dựa trên LSB cho ảnh BMP 8bits hoặc một định dạng khác như GIF [16]. Nhược điểm chính của giấu tin bằng LSB là dễ bị nén và biến dạng hình ảnh khi có các cuộc tấn công, dẫn đến dữ liệu được trích xuất không chính xác [17, 18]. Hoạt động giấu tin bằng LSB được thể hiện qua công thức sau:
Y_i=2⌊X_i/2⌋+m_i 			(1)
Trong đó, mi, Xi, Yi lần lượt là bit dữ liệu thứ i được nhúng vào ảnh, giá trị của điểm ảnh trước và sau khi nhúng.
Ví dụ, chúng ta có 3 điểm ảnh với mỗi điểm ảnh được tạo thành từ 3 byte màu đỏ, xanh lam, xanh lục (Hình 2). Mỗi Byte của ảnh có thể giấu được 1 bit dữ liệu, do đó chúng ta có thể nhúng được 9 bits dữ liệu bí mật [19]. Các bit màu đỏ ở Hình 2 thể hiện các bit dữ liệu ẩn “100010111”. Tuy nhiên, trên thực tế không phải toàn bộ các bit LSB bị thay đổi, do một số bit LSB có giá trị trùng với giá trị của bit dữ liệu nhúng không bị thay đổi. 
 
Hình 2. Giấu 9 bits dữ liệu trong 3 điểm ảnh
Các phương pháp giấu tin dựa trên nhiều mặt phẳng bit 
Giấu tin trong ảnh bằng phương pháp LSB thông thường có thể dẫn đến sự biến đổi giá trị của nhiều bit trong ảnh chứa, từ đó, có thể dễ dàng bị phát hiện. Trong nghiên cứu của Kawaguchi và Eason [20] đã đề xuất kỹ thuật độ phân đoạn phức tạp mặt phẳng bit bằng cách chuyển đổi ảnh đã được mã hóa nhị phân sang dạng ảnh mã hóa Gray chuẩn, sau đó chia thành một tập hợp các ảnh nhị phân theo mặt phẳng bit. Với mỗi mặt phẳng bit mã hóa Gray chuẩn, ảnh nhị phân được tách thành các khối liên tiếp không chồng chéo. Với kỹ thuật này, có thể đạt được được 4bpp mà không gây ra hiện tượng nhiễu.  
Trong nhóm phương pháp giấu tin trong miền không gian, dựa trên kỹ thuật LSB, nhiều tác giả đã sử dụng một số thay đổi nhỏ nhằm tránh được sự tấn công bằng thống kê cặp giá trị [21-23], hoặc có thể giấu tin dựa trên dự đoán lỗi [24] và lượng tử hóa [25].
	Các phương pháp giấu tin trong miền tần số
Các thuật toán giấu tin trong miền không gian thường có sức chống chịu sự tấn công và thám mã, do vậy, với nhu cầu nâng cao hiệu suất, các nhà khoa học đã đề xuất các thuật toán giấu tin trong miền tần số. Phương pháp này phù hợp với các định dạng ảnh JPEG, với việc nhúng dữ liệu ẩn vào các hệ số biến đổi cosin rời rạc, DCT (Discrete Cosin Transform). Tốc độ nhúng dữ liệu thường được tính bằng bit trên mỗi hệ số DCT khác không. Biến đổi cosin rời rạc được sử dụng rộng rãi trong nén ảnh và video. Mỗi khối hệ số DCT thu được đều được lượng tử hóa thông qua bảng lượng tử QT (Quantum Table). 
 
Hình 3. Quy trình giấu tin trong miền tần số
Hình 3 thể hiện quy trình giấu tin trong miền tần số với các ảnh JPEG. Đầu tiên, bức ảnh được phân tách thành các khối có kích thước 8 x 8, sau đó mỗi khối này được biến đổi cosine rời rạc và chuyển thành các bảng lượng tử hóa. Dữ liệu ẩn sẽ được nhúng vào bảng lượng tử hóa này. Tiếp đến, các khối dữ liệu được nén với thuật toán nén dữ liệu Huffman, dựa trên bảng Huffman table để tạo thành các khối 8 x 8 của ảnh chứa dữ liệu bí mật và được nén lại.    
Trong nhóm các phương pháp này, JSteg [26] và JPHide [27] sử dụng kỹ thuật nhúng dữ liệu LSB. Jsteg ẩn dữ liệu bí mật vào ảnh bằng cách thay thế tuần tự các LSB của các hệ số DCT lượng tử khác không bằng các bit dữ liệu bí mật. JPHide sử dụng một bộ tạo mã ngẫu nhiên và được điều khiển bằng một khóa bí mật. JPHide không chỉ thay đổi các LSB của các hệ số mà còn có thể chuyển sang chế độ thay đổi các bit của mặt phẳng bit có trọng số thấp thứ hai. 
Năm 2001, Westfield đưa ra thuật toán F5 [28], nhúng các bit dữ liệu vào các hệ số DCT được chọn ngẫu nhiên, và nhúng ma trận để giảm thiểu số lượng sửa đổi cần thiết để che giấu dữ liệu có độ dài nhất định. 
Thuật toán YASS (Yet Another Steganographic Scheme) được trình bày vào năm 2007 [29], ảnh đầu vào được tách thành các khối có kích thước lớn cố định, và các khối này được tên là khối lớn (B-blocks). Mỗi khối B này lại được chia thành các khối phụ 8 x 8, gọi là các khối H (H-blocks). Dữ liệu nhúng được mã hóa với các bits sửa lỗi và nhúng vào các hệ số DCT của các khối H bằng điều chế QIM (Quantum Index Modulation). Bằng hình thức chèn thêm bit sửa lỗi, dữ liệu mật được trích xuất sẽ được bảo toàn. 
Dựa trên biến đổi sóng rời rạc, DWT (Discrete Wavelet Tranform), Abdelwahab và Hassan [30] đề xuất một thuật toán giấu tin bằng cách giải nén ảnh mật và ảnh gốc sử dụng DWT. Các tác giả chia ảnh thành các khối rời rạc 4 x 4 và các khối của ảnh bí mật phù hợp để xác định việc nhúng tốt nhất. 
	Đánh giá chất lượng hình ảnh
Tham số chính để đánh giá chất lượng hình ảnh trong các thuật toán giấu tin và thủy vân số là PSNR (Peak Signal-to-Noise Rate) và SSIM (Structural Similarity) [31]. PSNR là tỷ lệ tín hiệu nhiễu được tính theo công thức sau:
 
(2)
Trong  đó,  MSE là sai số bình phương trung bình, được tính bằng, 
 
(3)
Với m, n là hàng và cột của ảnh gốc, F là ảnh gốc, N là ảnh sau khi nhúng dữ liệu và là xấp xỉ nhiễu của F.
Chỉ số SSIM được sử dụng để đo chất lượng video. Trong nghiên cứu này, chỉ số SSIM giữa ảnh gốc và ảnh nhúng được tính theo công thức sau:
 
(4)
trong đó Oi và Ei biểu thị  khối độ sáng  4×4 trong ảnh gốc và ảnh nhúng; N là số 4×4 khối độ sáng;   và  biểu thị phương sai trung bình của O và E;  là hiệu phương sai của O và E; c1 = (k1×L)2 và c2 = (k2×L)2  với L=255, k1, k2 là các giá trị trong khoảng từ 0.001 đến 0.009. 
	Cải thiện bảo mật trong giấu tin
Có một số yếu tố ảnh hưởng đến bảo mật trong giấu tin như số lượng pixel/hệ số sửa đổi, tính chất của ảnh gốc, biên độ của nhiễu tín hiệu. 
	Tăng hiệu suất nhúng dữ liệu
Hiệu quả nhúng dữ liệu được định nghĩa là số lượng bit nhúng cho mỗi một sự thay đổi. Vì vậy, để nâng cao hiệu quả nhúng, một số nghiên cứu thực hiện bằng việc tách thành các nhóm hệ số, sau đó sử dụng mã sửa lỗi Hamming hoặc mã BCH để có thể chịu đựng được các sự tấn công làm méo mó dữ liệu nhúng. Mã Hamming sử dụng k bit sửa lỗi cho m bit dữ liệu để tạo thành mã (k+m, m). Ví dụ, mã Hamming (11, 7) cần sử dụng 4 bits sửa lỗi cho 7 bits dữ liệu. 
Giả sử chúng ta nhận được chuỗi giá trị nhị phân 11011011011, chúng ta cần kiểm tra xem bits dữ liệu nào có thể bị lỗi
 
Hình 4. Mã sửa lỗi Hamming
Hình 4 thể hiện việc kiểm tra lỗi bit trong thuật toán Hamming. Việc kiểm tra được thực hiện theo quy luật: Bắt đầu từ vị trí x, kiểm tra x bits, bỏ qua x bits,.. cho đến khi hết độ dài từ mã. Vị trí lỗi được tính bằng cách cộng các vị trí bắt đầu kiểm tra nếu số bits 1 trong được kiểm tra là lẻ. Trong ví dụ trên, các vị trí bắt đầu kiểm tra gây ra số bits 1 lẻ là (1), (2) và (4), do đó, vị trí bit lỗi là 1+2+4=7. Để sửa lỗi, chúng ta chỉ cần đảo bit của bit lỗi từ 1 sang thành 0. 
Như vậy, với cách thức sử dụng mã sửa lỗi Hamming thì giả sử có bị lỗi bit thì dữ liệu ẩn có thể khôi phục được. 
	Giảm thiểu biến dạng của dữ liệu nhúng
Việc nâng cao hiệu quả nhúng có thể dẫn đến sự gia tăng biến dạng của ảnh chứa. Giấu tin dựa trên rối lượng tử (Pertubed Quantunzation - PQ)  [32] thực hiện bằng cách thay đổi một số hệ số mà lỗi lượng tử là nhỏ nhất sau khi nhúng dữ liệu. Kỹ thuật này có thể được sử dụng trong quá trình giảm dữ liệu bao gồm lượng tử hóa và biến đổi, như thay đổi kích thước và nén ảnh JPEG. Phương pháp giấu tin dựa trên ma trận mã hóa sửa đổi (Modified Matrix Encoding - MME) [33] thay đổi các hệ số mà lỗi lượng tử và lỗi nhúng dữ liệu nhỏ nhất trong quá trình nén ảnh JPEG. Ảnh chưa được nén được sử dụng làm đầu vào và sử dụng mã hóa ma trận trong quá trình nhúng dữ liệu. 
Như vậy, giảm thiểu biến dạng sau khi nhúng dữ liệu thường sử dụng trong các phương pháp giấu tin trong miền tần số với ảnh số định dạng JPEG.   
	Các đặc điểm của các kỹ thuật giấu tin
Mỗi phương pháp giấu tin khác nhau thường có những đặc điểm chính. Bảng 1 trình bày các đặc điểm chính trong mỗi phương pháp giấu tin. 
Phương pháp giấu tin	Các đặc điểm
LSB	Thay thế bit có trọng số nhỏ nhất
LSB Matching	Tăng hoặc giảm 1 ngẫu nhiên
Stochastic Modulation	Điều chế dữ liệu nhúng dưới dạng tín hiệu nhiễu
QIM/DM	Lượng tử hóa được xác định bởi bit dữ liệu (thường trong miền biến đổi)
PVD	Dữ liệu được nhúng trong sự khác biệt với điểm ảnh lân cận
JSteg	Sử đổi bit có trọng số nhỏ nhất trong các hệ số DCT
MB	Giữ lại các mô hình có độ chính xác thấp
F5	Giảm các giá trị hệ số tuyệt đối và sử dụng ma trận nhúng 
YASS	Sử dụng vị trí ngẫu nhiên

	Kết luận
Bài báo này đã thảo luận tổng quan về các phương pháp giấu tin trong ảnh. Các phương pháp dựa trên miền không gian có thể dễ bị phát hiện và có khả năng chống chịu với việc chuyển đổi và nén ảnh. Do vậy, các kỹ thuật này thường được sử dụng với các ảnh số không sử dụng kỹ thuật nén ảnh. Với các bức ảnh số JPEG sử dụng các kỹ thuật nén ảnh thì các phương pháp dựa trên miền không gian không khả dụng, vì trong quá trình nén ảnh thì sự biến dạng của ảnh sẽ dẫn đến sai sót dữ liệu sau khi trích xuất. Nhằm cải thiện chất lượng của dữ liệu nhúng và ảnh chứa dạng JPEG, các phương pháp dựa trên miền biến đổi cosin rời rạc (DCT) và biến đổi tần số sóng rời rạc (DWT) sửa đổi các hệ số trong miền biến đồi khi nhúng dữ liệu mật. Các phương pháp giấu tin dựa trên miền tần số thường có khả năng nhúng được ít hơn, song khả năng sai hỏng dữ liệu sau khi trích xuất cũng giảm thiểu đáng kể, đồng thời cũng mạnh mẽ khi chịu đựng các hình thức tấn công. 
Tài liệu tham khảo
[1] Hniels Provos & Peter Honeyman,”Hide & Seek: An Introduction to Steganography” IEEE Computer Society Pub-2003.
[2] Ge Huayong, Huang,”Steganography and Steganalysis Based on Digital Image”, International conference & signal Processing-2011, IEEE.
[3] N.F. Johnson and S. Jajodia, Exploring steganography: Seeing the unseen, IEEE Computer, 31(2) (1998) 26-34.
[4] J.C. Judge, Steganography: Past, present, future. SANS Institute	publication, http://www.sans.org/reading_room/whitepapers/stengano graphy/552.php, 2001.
[5] M. Swanson, M. Kobayashi, and A. Tewfik, “Multimedia data     embedding     and     watermarking     technologies,” Proceedings of the IEEE, Vol. 86, No. 6, pp. 1064-1087, June 1998.
[6] P. Wayner, Disappearing Cryptography, second ed, Morgan Kaufmann Publishers, 2002.
[7] R. Wolfgang, C. Podilchuk and E. Delp, “Perceptual watermarks for images and video,” to appear in the Proceedings of the IEEE, May, 1999. (A copy of this paper is available at: http://www.ece.purdue.edu/~ace).
[8] N. Johnson and S. Jajodia, “Exploring steganography: seeing the unseen,” IEEE Computer, pp. 26-34, February 1998.
[9]   Li, F., Hu, H., Zhu, S., Yan, J., & Ding, J. (2022). A verifiable (k, n)-threshold dynamic quantum secret sharing scheme. Quantum Information Processing, 21(7).
[10] J.	Flores‐Escalante,	J.	Pérez‐Díaz	and	R. Gómez‐Cárdenas, Design and Implementation of An Electronic Identification Card, Journal Of Applied Research And Technology
[11] Aravind K. Mikkilineni, Osman Arslan , Pei-Ju Chiang, Roy M. Kumontoy, Jan P. Allebach,George T.-C.Chiu, Edward     J.     Delp,     Printer     Forensics     using     SVM Techniques , This research was supported by a grant from the National Science Foundation, under Award Number 0219893
[12] M. Wu, E. Tang, and B. Lin, Data hiding in digital binary image, Proc. of 2000 IEEE International Conference on Multimedia and Expo,vol. 1, pp. 393-396, 2000.
[13] G. Liang, S. Wang, and X. Zhang, Steganography in binary image by checking data-carrying eligibility of boundary pixels, Journal of Shanghai University, vol. 11, no. 3, pp. 272-277, 2007.
[14] Jessica Fridrich, Miroslav Goljan, and Rui Du, Reliable detection of lsb steganography in color and Gray scale images. Proc. of 2001 ACM workshop on Multimedia and security: new challenges, pp.27-30, ACM Press, 2001.
[15] P. Alvarez, Using extended file information (EXIF) file headers in digital evidence analysis, International Journal of Digital Evidence, Economic Crime Institute (ECI) 2 (3) (2004) 1–5.
[16] V. Lokeswara Reddy, Dr.A.Subramanyam, Dr.P. Chenna Reddy, “Implementation of LSB Steganography and its Evaluation for Various File Formats”, Int. J. Advanced Networking and Applications 868 Volume: 02, Issue: 05, Pages: 868-872 (2011)
[17] Morkel, T., Eloff, J.H.P., Olivier, M.S.: An Overview of Image Steganography. University of Pretoria, South Africa (2002)
[18] Wang, H., Wang, S.: Cyber Warfare: Steganography vs. Steganalysis. Communications of the ACM 47(10) (2004)
[19] T. Morkel, JHP Eloff and MS Olivier, "An Overview of Image Steganography," in Proceeding of the Fifth Annual Information Security South Africa Conference (ISSA2005), Sand to South Africa, June/July 2005
[20] Eiji Kawaguchi and Richard O. Eason, Principle and applications of bpcs steganography, In Multi-media Systems and Applications, vol. 3528, pp. 464-473, SPIE, 1998.
[21] T. Sharp, An implementation of key-based digital signal steganography, Proc. of the 4th Information Hiding Workshop, vol. 2137, pp. 13-26, Springer, 2001.
[22] J. Mielikainen,Lsb matching revisited, IEEE Signal Processing Letters, vol. 13, no. 5, pp. 285-287, 2006.
[23] X. Li, B. Yang, D. Cheng, and T. Zeng, A generalization of lsb matching, IEEE Signal Processing Letters, vol. 16, no. 2, pp. 69-72, 2009.
[24] D. C. Wu and W. H. Tsai, A steganographic method for images by pixel-value diRerencing, Pattern Recognition Letters, vol. 24, no. 9-10, pp. 1613-1626, 2003.
[25] B. Chen and G. W. Wornell, Quantization index modulation: A class of provably good methods for digital watermarking and information embedding, IEEE Trans. Information Theory, vol. 47, no. 4, pp. 1423-1443, 2001.
[26] Qiao, T., Retraint, F., Cogranne, R., & Zitzmann, C. (2015). Steganalysis of JSteg algorithm using hypothesis testing theory. EURASIP Journal on Information Security, 2015(1), 2.
[27] Borghys, D., Bas, P., & Bruyninckx, H. (2018, June). Facing the cover-source mismatch on jphide using training-set design. In Proceedings of the 6th ACM Workshop on Information Hiding and Multimedia Security (pp. 17-22).
[28] A. Westfeld, F5-A steganographic algorithm: high capacity despite better steganalysis, in: Proceedings of Fourth International Work-shop on Information Hiding, Lecture Notes in Computer Science, vol. 2137, Pittsburgh, USA, April 2001, pp. 289–302.
[29] K. Solanki, A. Sarkar, and B. S. Manjunath, Yass: Yet another steganographic scheme that     resists blind steganalysis, Proc. of the 9th Information Hiding Workshop, Springer, vol. 4567, pp. 16-31, 2007.
[30] A.A. Abdelwahab, L.A. Hassan, A discrete wavelet transform based technique for image data hiding, in: Proceedings of 25th National Radio Science Conference, NRSC 2008, Egypt, March 18–20, 2008, pp. 1–9.
[31] Setiadi, D. R. I. M. (2021). PSNR vs SSIM: imperceptibility quality assessment for image steganography. Multimedia Tools and Applications, 80(6), 8423-8444.
[32] J. Fridrich, Feature-based steganalysis for jpeg images and its implications for future design of steganographic schemes, Proc. of the 6th Information Hiding Workshop, Springer, vol. 3200 , pp. 67-81, 2004.
[33] Y. Kim, Z. Duric, and D. Richards, Modified matrix encoding for minimal distortion steganography. Proc. of the 8th Information Hiding Workshop, Springer, vol. 4437, pp. 314-327, 2006.
 
<img width="425" height="673" alt="image" src="https://github.com/user-attachments/assets/f7220cb5-93cd-4aa0-b897-849891b485bc" />

