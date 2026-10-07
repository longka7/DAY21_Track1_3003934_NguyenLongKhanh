# Lab 21 — Phân tích rủi ro AI qua case study thực tế

- Họ và tên: Nguyễn Long Khánh
- MSSV / mã học viên: 3003934
- Lớp: H201
- Ngành đã chọn: HR / tuyển dụng (AI sàng lọc CV, đánh giá hoặc hỗ trợ tuyển ứng viên)

### 1. Industry Risk Snapshot

| Nội dung | Đánh giá của tôi và lý do |
| --- | --- |
| Những tác hại chính có thể xảy ra | Ứng viên đủ năng lực bị loại bất công do AI học lại thiên lệch giới, tuổi, chủng tộc hoặc khuyết tật từ dữ liệu tuyển dụng lịch sử; người bị ảnh hưởng là ứng viên cá nhân (mất cơ hội việc làm, thu nhập), còn doanh nghiệp dùng AI chịu rủi ro pháp lý và uy tín. |
| Mức độ high-stakes | Cao. Kết quả sàng lọc ảnh hưởng trực tiếp đến thu nhập và sự nghiệp của một người; nhiều hệ thống loại hồ sơ ngay từ vòng đầu, trước khi có người thật xem xét lại, nên ứng viên thường không biết và không có cơ hội giải trình. |
| Dữ liệu nhạy cảm có thể được sử dụng | Thông tin nhân khẩu học gắn với hồ sơ (ngày sinh/tuổi, giới tính, tên trường học có thể gắn với giới hoặc chủng tộc), và các đặc điểm nhạy cảm bị suy luận gián tiếp từ CV (ví dụ khoảng trống thời gian làm việc có thể liên quan đến tình trạng sức khỏe hoặc chăm sóc gia đình). Không đưa dữ liệu ứng viên thật vào bài. |
| Nhu cầu human review | Cao. Cần người có chuyên môn tuyển dụng và tuân thủ pháp lý kiểm tra kết quả xếp hạng/loại hồ sơ trước khi ra quyết định từ chối cuối cùng, và cần audit định kỳ để phát hiện thiên lệch hệ thống trước khi triển khai rộng. |

### 2. Case study 1 — Công cụ AI tuyển dụng nội bộ của Amazon

#### Brief Case

- Tổ chức / sản phẩm AI: Amazon — công cụ chấm điểm/xếp hạng hồ sơ ứng viên nội bộ (dự án từ năm 2014).
- Thời gian, địa điểm / bối cảnh: Phát triển 2014–2017 tại Seattle, Mỹ; bị Reuters tiết lộ công khai ngày 10/10/2018.
- AI được dùng để làm gì: Chấm điểm và xếp hạng tự động hồ sơ ứng viên cho các vị trí kỹ thuật (ví dụ software developer) dựa trên mô hình học từ hồ sơ nộp trong 10 năm trước đó.
- Vấn đề hoặc sự kiện đáng chú ý: Mô hình tự học rằng hồ sơ nam giới "tốt hơn" vì phần lớn dữ liệu huấn luyện là hồ sơ nam; nó hạ điểm hồ sơ chứa từ "women's" (ví dụ "women's chess club captain") và hạ điểm hồ sơ của người tốt nghiệp hai trường đại học chỉ dành cho nữ. Amazon chỉnh sửa để trung lập với các từ khóa cụ thể này, nhưng không có gì đảm bảo mô hình không tìm ra cách phân biệt khác; dự án bị giải thể đầu năm 2017.
- Số liệu có nguồn: Mô hình được huấn luyện trên dữ liệu hồ sơ ứng viên nộp trong khoảng 10 năm trước 2015, theo lời 5 người liên quan trực tiếp đến dự án được Reuters dẫn lại; đội dự án bị giải thể vào đầu năm 2017.
- Nguồn: "Amazon scraps a secret AI recruiting tool that showed bias against women" — CNBC (dẫn lại điều tra độc quyền của Reuters) — 10/10/2018 — https://www.cnbc.com/2018/10/10/amazon-scraps-a-secret-ai-recruiting-tool-that-showed-bias-against-women.html
- Phân biệt bằng chứng và nhận định: Nguồn xác nhận hiện tượng thiên lệch được chính các kỹ sư Amazon phát hiện nội bộ và công cụ bị dừng trước khi triển khai đại trà; nguồn không công bố số lượng hồ sơ cụ thể bị ảnh hưởng hay việc công cụ này có từng là cơ sở duy nhất để loại ứng viên thật hay chưa — phần này tôi ghi là chưa đủ dữ liệu để đánh giá quy mô thực tế.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Thời điểm hệ thống AI chấm điểm và xếp hạng hồ sơ ứng viên kỹ thuật, trước khi hồ sơ đến tay người tuyển dụng. |
| Stakeholder bị ảnh hưởng | Ứng viên nữ ứng tuyển vị trí kỹ thuật tại Amazon (đặc biệt người tốt nghiệp các trường đại học nữ); gián tiếp ảnh hưởng uy tín và nghĩa vụ tuân thủ pháp lý của Amazon. |
| Failure mode | Bias / fairness — mô hình học từ dữ liệu lịch sử lệch giới nên tự suy ra các tín hiệu liên quan đến nữ giới là tiêu cực. |
| Layer bắt đầu lỗi | Grounding (dữ liệu huấn luyện không đại diện cân bằng giới tính) kết hợp Model (thuật toán tổng quát hóa quá mức từ các đặc điểm liên quan giới tính); chưa đủ bằng chứng để xác định có lỗi ở lớp Safety hay không vì không rõ công cụ có cơ chế kiểm soát thiên lệch nào trước khi bị dừng. |
| Harm xảy ra là gì? | Đây chủ yếu là một nguy cơ được phát hiện và chặn lại nội bộ: nguồn xác nhận hiện tượng hạ điểm hồ sơ liên quan nữ giới có thật, nhưng không xác nhận có ứng viên cụ thể nào đã bị loại hoàn toàn chỉ vì công cụ này trước khi dự án dừng năm 2017. |
| Harm lens | Opportunity loss (mất cơ hội việc làm/thăng tiến nếu công cụ được dùng để ra quyết định). |
| Severity | High — nếu được triển khai đại trà, ảnh hưởng trực tiếp đến cơ hội nghề nghiệp và thu nhập của ứng viên nữ. |
| Scale | Chưa đủ dữ liệu để đánh giá số người cụ thể bị ảnh hưởng; quy mô tiềm năng cao vì hệ thống được thiết kế để xử lý toàn bộ hồ sơ kỹ thuật nội bộ của Amazon trong nhiều năm. |
| Probability | Cao trong giai đoạn hệ thống hoạt động (2014–2017), vì đây là một đặc điểm mang tính hệ thống của mô hình, không phải lỗi ngẫu nhiên — theo mô tả của nhiều kỹ sư liên quan trong nguồn. |
| Frequency | Nếu hệ thống được dùng, lỗi sẽ lặp lại ở mọi hồ sơ có chứa tín hiệu liên quan đến giới tính; đây là nhận định dựa trên bản chất thuật toán, chưa có số liệu tần suất cụ thể được công bố. |
| Vì sao? | Reuters dẫn 5 nguồn nội bộ xác nhận hiện tượng tồn tại và được Amazon tự phát hiện, khắc phục một phần; không có số liệu định lượng công khai về số hồ sơ bị ảnh hưởng thực tế, nên các đánh giá Scale/Probability dựa trên tính hệ thống của lỗi hơn là số liệu đếm được. |

### 3. Case study 2 — iTutorGroup bị EEOC kiện vì phần mềm tuyển dụng phân biệt tuổi tác

#### Brief Case

- Tổ chức / sản phẩm AI: iTutorGroup — công ty dạy tiếng Anh trực tuyến, dùng phần mềm tuyển dụng tự động để sàng lọc ứng viên gia sư.
- Thời gian, địa điểm / bối cảnh: Phần mềm hoạt động và từ chối ứng viên trong tháng 3–4/2020 tại Mỹ; Ủy ban Cơ hội Việc làm Bình đẳng Hoa Kỳ (EEOC) kiện và đạt thỏa thuận dàn xếp công bố ngày 09/08/2023 tại Tòa án Quận Đông New York.
- AI được dùng để làm gì: Tự động sàng lọc và loại hồ sơ ứng viên dạy gia sư trực tuyến dựa trên ngày sinh khai trong đơn ứng tuyển.
- Vấn đề hoặc sự kiện đáng chú ý: Phần mềm được lập trình để tự động từ chối ứng viên nữ từ 55 tuổi trở lên và ứng viên nam từ 60 tuổi trở lên, mà không có người thật xem xét lại trước khi loại hồ sơ.
- Số liệu có nguồn: Hơn 200 ứng viên đủ điều kiện tại Mỹ bị tự động từ chối vì tuổi trong các đơn nộp tháng 3–4/2020, theo hồ sơ vụ kiện của EEOC; mức dàn xếp là 365.000 USD.
- Nguồn: "EEOC Settles Its First Discrimination Lawsuit Involving Artificial Intelligence Hiring Software" — Duane Morris Class Action Defense Blog (dẫn Consent Decree nộp tại tòa) — 11/08/2023 — https://blogs.duanemorris.com/classactiondefense/2023/08/11/eeoc-settles-its-first-discrimination-lawsuit-involving-artificial-intelligence-hiring-software/
- Phân biệt bằng chứng và nhận định: Số liệu 200+ ứng viên và mức dàn xếp 365.000 USD là bằng chứng đã được xác nhận chính thức qua thỏa thuận pháp lý (Consent Decree) giữa EEOC và iTutorGroup, không phải suy đoán; nguồn không công khai tên hay chi tiết từng ứng viên cụ thể.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Thời điểm phần mềm tuyển dụng quét ngày sinh trong hồ sơ và tự động loại ứng viên trước khi hồ sơ được chuyển cho người tuyển dụng xem xét. |
| Stakeholder bị ảnh hưởng | Hơn 200 ứng viên tại Mỹ (phụ nữ ≥55 tuổi, nam giới ≥60 tuổi) ứng tuyển vị trí gia sư trực tuyến; iTutorGroup chịu trách nhiệm pháp lý, thiệt hại tài chính và uy tín. |
| Failure mode | Bias / fairness kết hợp Escalation failure — hệ thống tự động loại ứng viên dựa trên tuổi mà không chuyển cho người thật xem xét trước khi từ chối. |
| Layer bắt đầu lỗi | Grounding/Safety — tiêu chí loại theo tuổi được lập trình sẵn như một quy tắc trong hệ thống, không có lớp bảo vệ nào chặn tiêu chí phân biệt tuổi tác bất hợp pháp trước khi áp dụng. |
| Harm xảy ra là gì? | Đã xảy ra: theo Consent Decree, hơn 200 ứng viên đủ điều kiện bị tự động từ chối chỉ vì tuổi, mất cơ hội việc làm thực tế; đây là hậu quả đã được xác nhận pháp lý, không phải nguy cơ giả định. |
| Harm lens | Opportunity loss (mất cơ hội việc làm) kết hợp dignity loss (bị phân biệt đối xử dựa trên đặc điểm được pháp luật bảo vệ). |
| Severity | High — vi phạm luật chống phân biệt tuổi tác liên bang Mỹ (ADEA), dẫn đến hậu quả pháp lý và tài chính thực tế cho cả ứng viên và công ty. |
| Scale | Trung bình — hơn 200 ứng viên được xác nhận trong hồ sơ vụ kiện, giới hạn trong hai tháng (3–4/2020) tại Mỹ; chưa có số liệu công khai cho các giai đoạn hoặc thị trường khác. |
| Probability | Cao (gần như chắc chắn đối với nhóm đúng tiêu chí tuổi) vì đây là quy tắc được lập trình sẵn, áp dụng tự động cho mọi hồ sơ thỏa điều kiện. |
| Frequency | Diễn ra với mọi hồ sơ nộp trong giai đoạn tháng 3–4/2020 thỏa điều kiện tuổi — tần suất cao trong giai đoạn đó, theo hồ sơ vụ kiện; chưa rõ tần suất ở các giai đoạn khác. |
| Vì sao? | Số liệu 200+ ứng viên và mức dàn xếp 365.000 USD được xác nhận trong Consent Decree nộp tại tòa và được nhiều nguồn pháp lý đưa tin; đây là hậu quả đã xảy ra và được xác nhận chính thức, nên severity và probability được đánh giá cao với căn cứ rõ ràng. |

### 4. Case study 3 — Mobley v. Workday: kiện tập thể về thuật toán sàng lọc ứng viên

#### Brief Case

- Tổ chức / sản phẩm AI: Workday, Inc. — nhà cung cấp phần mềm quản trị nhân sự có công cụ sàng lọc/xếp hạng ứng viên bằng AI (algorithm-based applicant screening), được nhiều doanh nghiệp khách hàng sử dụng.
- Thời gian, địa điểm / bối cảnh: Đơn khởi kiện nộp lần đầu tháng 2/2023 tại Tòa án Quận Bắc California, Mỹ; tháng 7/2024 thẩm phán Rita Lin bác một phần yêu cầu bác đơn của Workday, cho phép vụ kiện tiến hành; đầu năm 2025 thẩm phán cho phép khiếu nại phân biệt tuổi tác tiến hành dưới dạng hành động tập thể quy mô toàn quốc.
- AI được dùng để làm gì: Sàng lọc và xếp hạng tự động hồ sơ ứng viên nộp qua các doanh nghiệp khách hàng dùng nền tảng tuyển dụng của Workday.
- Vấn đề hoặc sự kiện đáng chú ý: Nguyên đơn Derek Mobley — người Mỹ da đen, trên 40 tuổi, có tình trạng trầm cảm và lo âu — cáo buộc đã ứng tuyển 80–100 vị trí dùng Workday từ năm 2018 và không được nhận vào bất kỳ vị trí nào; đơn kiện cho rằng thuật toán của Workday gây tác động phân biệt (disparate impact) theo chủng tộc, tuổi tác và khuyết tật, dù không có chủ đích phân biệt trực tiếp. Vụ kiện vẫn đang trong giai đoạn tố tụng, chưa có phán quyết cuối cùng về việc có phân biệt hay không.
- Số liệu có nguồn: Nguyên đơn khai đã nộp 80–100 đơn ứng tuyển dùng hệ thống Workday từ năm 2018 đến khi khởi kiện mà không trúng tuyển vị trí nào, theo hồ sơ vụ kiện; tháng 7/2024, tòa cho phép vụ kiện tiến hành sang giai đoạn điều tra (discovery); đầu 2025, khiếu nại phân biệt tuổi tác (áp dụng cho ứng viên từ 40 tuổi) được cho phép tiến hành dưới dạng tập thể toàn quốc.
- Nguồn: "Discrimination Lawsuit Over Workday's AI Hiring Tools Can Proceed as Class Action: 6 Things to Know" — Fisher Phillips — https://www.fisherphillips.com/en/news-insights/discrimination-lawsuit-over-workdays-ai-hiring-tools-can-proceed-as-class-action-6-things.html
- Phân biệt bằng chứng và nhận định: Số lần ứng tuyển (80–100) và các mốc tố tụng là nội dung được xác nhận trong hồ sơ tòa án và các bài phân tích pháp lý; việc thuật toán của Workday "có" gây tác động phân biệt hay không vẫn là cáo buộc đang được tòa xem xét ở giai đoạn điều tra, chưa phải phán quyết cuối cùng — tôi ghi rõ đây là nguy cơ/cáo buộc, không phải kết luận đã được chứng minh.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Thời điểm thuật toán của Workday chấm điểm và tự động xếp hạng/loại hồ sơ ứng viên trước khi người tuyển dụng của doanh nghiệp khách hàng xem xét. |
| Stakeholder bị ảnh hưởng | Derek Mobley và nhóm ứng viên tập thể (người từ 40 tuổi trở lên, có thể gồm người da đen và người khuyết tật) ứng tuyển vào các công ty dùng Workday; các doanh nghiệp khách hàng của Workday chịu rủi ro liên đới pháp lý; Workday chịu rủi ro pháp lý và uy tín. |
| Failure mode | Bias / fairness — đơn kiện cáo buộc thuật toán gây tác động phân biệt (disparate impact) theo tuổi, chủng tộc và khuyết tật dù không có chủ đích phân biệt trực tiếp. |
| Layer bắt đầu lỗi | Chưa đủ bằng chứng công khai để xác định chính xác, vì thuật toán và dữ liệu huấn luyện của Workday không được công bố; giả thuyết đang được tòa xem xét là lớp Grounding/Model — mô hình có thể học từ dữ liệu tuyển dụng lịch sử phản ánh thiên lệch nhân khẩu học trong các quyết định tuyển dụng trước đó. |
| Harm xảy ra là gì? | Nguyên đơn khẳng định đã nộp 80–100 đơn ứng tuyển dùng Workday từ 2018 mà không trúng tuyển vị trí nào — đây là tác hại cụ thể được nêu trong hồ sơ vụ kiện; tòa cho phép vụ kiện tiến hành nên cáo buộc được xem là có cơ sở ban đầu, nhưng việc có thực sự bị phân biệt do thuật toán hay không vẫn chưa được phán quyết cuối cùng xác nhận. |
| Harm lens | Opportunity loss (mất cơ hội việc làm); có thể kèm dignity loss nếu tòa xác nhận có phân biệt dựa trên đặc điểm được pháp luật bảo vệ. |
| Severity | High nếu cáo buộc được xác nhận — vì ảnh hưởng đến thu nhập và cơ hội nghề nghiệp lâu dài của hàng loạt ứng viên qua nhiều doanh nghiệp khách hàng. |
| Scale | Cao về tiềm năng — vụ kiện được cho phép tiến hành dưới dạng hành động tập thể toàn quốc Mỹ cho khiếu nại phân biệt tuổi tác, liên quan đến nhiều ứng viên ứng tuyển qua các công ty dùng Workday; chưa có số liệu tổng số người cụ thể được tòa xác nhận tại thời điểm này. |
| Probability | Chưa đủ dữ liệu để khẳng định tỷ lệ chính xác — vụ kiện đang ở giai đoạn điều tra (discovery) để xác định có tác động phân biệt thống kê rõ ràng hay không. |
| Frequency | Nếu có tác động phân biệt hệ thống, tần suất sẽ cao vì Workday xử lý khối lượng lớn đơn ứng tuyển cho nhiều doanh nghiệp mỗi ngày; đây là nhận định dựa trên quy mô sử dụng nền tảng, chưa có số liệu tần suất cụ thể được tòa xác nhận. |
| Vì sao? | Thông tin dựa trên hồ sơ vụ kiện công khai và phân tích pháp lý (Fisher Phillips và các nguồn liên quan); vụ kiện đang trong giai đoạn tố tụng nên nhiều kết luận về "đã có phân biệt hay chưa" còn là cáo buộc, không phải phán quyết cuối cùng — tôi giữ nguyên sự phân biệt này trong toàn bộ phần phân tích. |
