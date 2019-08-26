# LocalizableToExcel
Make easy to change Localizable.strings to Excel

// start from here

var str = """
// 공통
"알림" = "Thông báo";
"확인" = "Xác nhận";
"취소" = "Hủy";
"닫기" = "Đóng";
"삭제" = "Xóa";
"더보기" = "Xem thêm";
"완료" = "Đã hoàn thành";
"종료" = "Kết thúc";
"설정" = "Cài đặt";

// 서버 통신
"사용자 확인 실패" = "Không thể xác minh người dùng";
"앱 재시작 후 다시 시도해주세요." = "Vui lòng khởi động lại ứng dụng của bạn và thử lại.";
"등록되지 않은 스탬프입니다." = "Con dấu chưa được đăng ký.";
"이미 받은 스탬프입니다. QR코드 스탬프는 첫 스탬프일때만 적립됩니다." = "Bạn đã nhận được con dấu. Bạn sẽ chỉ có được con dấu mã QR khi đó là con dấu đầu tiên";
"바우처 발행처와 스탬프 소유자가 일치하지 않습니다." = "  Người xuất Voucher và người sở hữu con dấu không khớp nhau";
"사용할 수 없는 바우처입니다. 바우처의 유효기간을 확인해 주세요." = "Vouchers không khả dụng. Vui lòng kiểm tra thời hạn sử dụng của Voucher";
"제주인 혜택을 제공하지 않는 샵입니다." = "Cửa hàng không đưa ra các lợi ích cho người dân Jeju";
"존재하지 않는 사용자입니다." = "Người dùng không tồn tại";
"요청한 API URL이 존재하지 않습니다." = "API URL được yêu cầu không tồn tại";
"업데이트 후 사용하실 수 있습니다." = "Bạn có thể sử dụng nó sau khi cập nhật";
"설정 버튼을 누르시면, 업데이트 화면으로 이동합니다." = "Ấn nút cài đặt, màn hình cập nhật sẽ hiện ra";
"서버 오류" = "Lỗi máy chủ";
"잠시 후 다시 시도해주세요." = "Vui lòng thử lại trong vài phút";
"스탬프 카드가 존재하지 않습니다." = "Thẻ con dấu không tồn tại";
"가맹점이 존재하지 않습니다." = "Đặc quyền kinh doanh không tồn tại.";
"스탬프 인증 간격은 최소 3분 입니다. 잠시 후 다시 시도해주세요." = "Thời gian ngừng để xác minh con dấu là ít nhất 3 phút. Vui lòng thử lại sau.";
"모바일 스탬프투어 참여는 1인 1회에 한하며 중복참여는 불가합니다." = "Không được phép tham gia vào Mobile Stamp Tour (Tour con dấu di động) hơn một người một lần.";

// 마이크 권한
"마이크 사용 권한이 없습니다." = "Bạn không được phép sử dụng microphone.";
"‘아이폰 > 설정 > yoyo stamp > 마이크 허용' 후 디지털 스탬프를 사용하실 수 있습니다." = " “Bạn có thể sử dụng con dấu điện tử sau khi thực hiện các bước ‘iPhone> Settings> YOYO Stamp> Accept Mike‘.";

// 위치 권한
"위치 서비스를 이용할 수 없습니다." = "Dịch vụ địa điểm (Location Services) không khả dụng.";
"아이폰 설정 > yoyo stamp > 위치 접근 허용 후 사용할 수 있습니다." = "Bạn có thể sử dụng định vị sau khi cho phép truy cập các bước IPhone Settings> YOYO Stamp>";
"아이폰 설정 > 개인 정보 보호 > 위치 서비스 활성화 후 사용할 수 있습니다." = "Bạn có thể sử dụng định vị sau khi kích hoạt các bước Iphone settings(Cài đặt Iphone) > Privacy (Bảo mật) > Định vị (Location Services).";

"""

enum Status {
    case stop
    case startStr1
    case readyStr2
    case startStr2
}

var status: Status = .stop

var str1 = String()
var str2 = String()
var char: Character!
var str1List = [String]()
var str2List = [String]()
while !str.isEmpty {
    char = str.removeFirst()
    if char == "\"" {
        switch status {
        case .stop:
            status = .startStr1
        case .startStr1:
            status = .readyStr2
        case .readyStr2:
            status = .startStr2
        case .startStr2:
            status = .stop
            str1List.append(str1)
            str2List.append(str2)
            str1 = ""
            str2 = ""
        }
    } else {
        switch status {
        case .stop:
            _ = 1
        case .startStr1:
            str1.append(char)
        case .readyStr2:
            _ = 1
        case .startStr2:
            str2.append(char)
        }
    }
}

for item in str1List {
    print(item)
}

for item in str2List {
    print(item)
}
