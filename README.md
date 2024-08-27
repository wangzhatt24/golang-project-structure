# Golang Project Structure

Cấu trúc thư mục cho dự án golang 

Đọc thêm tại: https://github.com/golang-standards/project-layout

Tại sao cần nó?

- Dễ bảo trì và mở rộng
- Dễ quản lý cấu hình
- Tăng khả năng tái sử dụng mã

```markdown
my-go-project/
├── cmd/                # Các ứng dụng chính của dự án
│   └── _your_app_/     # Thư mục cho ứng dụng chính
│       └── .keep
├── internal/           # Mã nguồn nội bộ không được phép sử dụng bởi các ứng dụng bên ngoài
│   ├── app/            # Thư mục ứng dụng nội bộ
│   │   └── _your_app_/ # Thư mục cho ứng dụng nội bộ
│   │       └── .keep
│   └── pkg/            # Thư viện nội bộ có thể tái sử dụng
│       └── _your_private_lib_/
│           └── .keep
├── pkg/                # Thư viện và gói có thể tái sử dụng công khai
│   └── _your_public_lib_/
│       └── .keep
├── api/                # Định nghĩa API và tài liệu liên quan
│   └── README.md
├── assets/             # Tài nguyên tĩnh, ví dụ hình ảnh, biểu tượng
│   └── README.md
├── build/              # Tài nguyên liên quan đến xây dựng và triển khai
│   ├── ci/             # Cấu hình liên quan đến tích hợp liên tục (CI)
│   │   └── .keep
│   └── package/        # Tài nguyên liên quan đến đóng gói
│       └── .keep
├── configs/            # Các tệp cấu hình cho ứng dụng
│   └── README.md
├── deployments/        # Tài nguyên và tài liệu liên quan đến triển khai
│   └── README.md
├── docs/               # Tài liệu dự án
│   └── README.md
├── examples/           # Ví dụ về cách sử dụng ứng dụng hoặc thư viện
│   └── README.md
├── githooks/           # Các hook Git tùy chỉnh
│   └── README.md
├── init/               # Tài nguyên liên quan đến việc khởi tạo dự án
│   └── README.md
├── scripts/            # Các script tiện ích cho phát triển hoặc triển khai
│   └── README.md
├── test/               # Tài nguyên kiểm thử bổ sung, kiểm thử tích hợp
│   └── README.md
├── third_party/        # Tài nguyên và mã nguồn của bên thứ ba
│   └── README.md
├── tools/              # Công cụ hỗ trợ phát triển
│   └── README.md
├── vendor/             # Các phụ thuộc của bên thứ ba được giữ lại bởi Go Modules
│   └── README.md
├── web/                # Các tệp liên quan đến giao diện người dùng hoặc trang web
│   ├── app/            # Ứng dụng web
│   │   └── .keep
│   ├── static/         # Tệp tĩnh như CSS, JavaScript, hình ảnh
│   │   └── .keep
│   └── template/       # Mẫu HTML hoặc template khác
│       └── .keep
├── website/            # Tài nguyên liên quan đến website
│   └── README.md
├── .editorconfig       # Cấu hình trình soạn thảo
├── .gitattributes      # Cấu hình thuộc tính Git
├── .gitignore          # Danh sách các tệp và thư mục bị loại trừ bởi Git
├── go.mod              # Tệp module quản lý các phụ thuộc Go
├── LICENSE.md          # Giấy phép sử dụng
├── Makefile            # Tập lệnh để tự động hóa các nhiệm vụ (xây dựng, thử nghiệm, v.v.)
└── README.md           # Tài liệu hướng dẫn sử dụng và thông tin dự án

```

Giải nghĩa nó:

```markdown
│   .editorconfig
│   .gitattributes
│   .gitignore
│   go.mod
│   LICENSE.md
│   Makefile
│   README.md
```

Cụm này thì có cái go.mod là sử dụng để quản lí phụ thuộc (thuộc go)

## Thư mục cmd

```markdown
cmd/
├── myapp/              # Thư mục cho ứng dụng chính
│   ├── main.go         # Điểm vào chính của ứng dụng
│   └── config.go       # Các cấu hình hoặc cài đặt ứng dụng
│
└── otherapp/           # Thư mục cho một ứng dụng khác (nếu có)
    ├── main.go         # Điểm vào chính của ứng dụng khác
    └── helper.go       # Các tiện ích hoặc chức năng hỗ trợ
```

Chứ các ứng dụng…

Tại sao phải cần nhiều ứng dụng như vậy?

Ví dụ ta cần chạy một ứng dụng chính, thêm vào đó cần một ứng dụng để xử lý dữ liệu, ứng dụng cli để tác vụ quản trị…

(Microservices)

## Thư mục internal

Nếu thư mục cần chứa mã nguồn chỉ sử dụng cho riêng project này thôi thì nó sẽ đặt ở đây.

```markdown
├── internal/           # Mã nguồn nội bộ không được phép sử dụng bởi các ứng dụng bên ngoài
│   ├── app/            # Thư mục ứng dụng nội bộ
│   │   └── _your_app_/ # Thư mục cho ứng dụng nội bộ
│   │       └── .keep
│   └── pkg/            # Thư viện nội bộ có thể tái sử dụng
│       └── _your_private_lib_/
│           └── .keep
```

## Thư mục pkg

Chứa các thư viện và gói mà có thể chia sẻ công khai với các dự án khác hoặc public nó ra cho cộng đồng.

```markdown
├── pkg/                # Thư viện và gói có thể tái sử dụng công khai
│   └── _your_public_lib_/
│       └── .keep
```

## Thư mục api

Tổ chức và lưu trữ mã nguồn liên quan đến các API của ứng dụng.

API là gì?

```markdown
api/
├── v1/
│   ├── handler.go       # Xử lý các yêu cầu API cho phiên bản 1
│   ├── router.go        # Định nghĩa các điểm cuối (endpoints) API
│   └── model.go         # Định nghĩa các mô hình dữ liệu cho API
│
├── v2/
│   ├── handler.go       # Xử lý các yêu cầu API cho phiên bản 2
│   ├── router.go        # Định nghĩa các điểm cuối (endpoints) API
│   └── model.go         # Định nghĩa các mô hình dữ liệu cho API
│
└── README.md            # Tài liệu hướng dẫn sử dụng và cấu hình API

```

## Thư mục assets

Chứa các tài nguyên tĩnh

```markdown
assets/
├── images/
│   ├── logo.png         # Hình ảnh logo
│   ├── background.jpg   # Hình nền
│   └── icon.svg         # Biểu tượng SVG
│
├── css/
│   ├── styles.css       # Tệp CSS chính
│   └── theme.css        # Tệp CSS cho các chủ đề
│
├── js/
│   ├── scripts.js       # Tệp JavaScript chính
│   └── analytics.js     # Tệp JavaScript cho phân tích
│
└── fonts/
    ├── custom-font.ttf  # Phông chữ tùy chỉnh
    └── icon-font.woff  # Phông chữ biểu tượng

```

## Thư mục build

Lưu trữ các tập tin và cấu hình liên quan đến quá trình xây dựng và triển khai dự án.

```markdown
build/
├── ci/
│   ├── docker/
│   │   ├── Dockerfile       # Tệp cấu hình Docker cho việc đóng gói ứng dụng
│   │   └── docker-compose.yml # Tệp cấu hình Docker Compose cho môi trường phát triển
│   ├── github/
│   │   └── workflows/
│   │       └── build.yml    # Tệp cấu hình GitHub Actions cho quá trình xây dựng và triển khai
│   └── jenkins/
│       └── Jenkinsfile      # Tệp cấu hình Jenkins cho quá trình xây dựng và triển khai
│
├── package/
│   ├── build.sh             # Script để xây dựng và đóng gói ứng dụng
│   └── release_notes.md     # Tài liệu ghi chú phát hành và thay đổi
│
└── README.md                # Tài liệu hướng dẫn sử dụng thư mục build

```

## Thư mục config

Lưu trữ các tệp cấu hình và tài liệu liên quan đến cấu hình ứng dụng.

```markdown
configs/
├── app.yaml              # Cấu hình chính cho ứng dụng
├── database.yml          # Cấu hình kết nối cơ sở dữ liệu
├── server.json           # Cấu hình máy chủ và cổng
├── logging.yml           # Cấu hình ghi log
└── README.md             # Tài liệu hướng dẫn sử dụng thư mục configs

```

## Thư mục deployment

Lưu trữ các tài liệu và cấu hình liên quan đến việc triển khai ứng dụng.

```markdown
deployments/
├── kubernetes/
│   ├── deployment.yaml      # Cấu hình triển khai cho Kubernetes
│   ├── service.yaml         # Cấu hình dịch vụ cho Kubernetes
│   └── ingress.yaml         # Cấu hình ingress cho Kubernetes
│
├── docker/
│   ├── docker-compose.yml   # Cấu hình Docker Compose cho triển khai
│   └── Dockerfile           # Dockerfile để xây dựng hình ảnh Docker
│
├── terraform/
│   ├── main.tf              # Tệp cấu hình Terraform chính
│   ├── variables.tf         # Tệp cấu hình biến Terraform
│   └── outputs.tf           # Tệp cấu hình đầu ra Terraform
│
└── README.md                # Tài liệu hướng dẫn triển khai

```

## Thư mục docs

Lưu trữ tài liệu liên quan đến dự án, hướng dẫn sử dụng, tài liệu API, tài liệu kĩ thuận

```markdown
docs/
├── api/
│   ├── index.md            # Tài liệu chính cho API
│   ├── authentication.md   # Hướng dẫn xác thực API
│   └── endpoints.md        # Tài liệu mô tả các điểm cuối API
│
├── guides/
│   ├── installation.md     # Hướng dẫn cài đặt
│   ├── usage.md            # Hướng dẫn sử dụng
│   └── troubleshooting.md  # Hướng dẫn khắc phục sự cố
│
├── architecture.md         # Tài liệu kiến trúc hệ thống
├── changelog.md            # Ghi chú phát hành và thay đổi
└── README.md               # Tài liệu hướng dẫn chung về dự án

```

## Thư mục examples

Sử dụng để lưu trữ các ví dụ mã hoặc mẫu giúp người dùng hiểu cách sử dụng thư viện hoặc ứng dụng.

```markdown
examples/
├── basic_usage/
│   ├── example1.go        # Ví dụ đơn giản về cách sử dụng thư viện
│   ├── example2.py        # Ví dụ bằng ngôn ngữ khác, nếu cần
│   └── README.md          # Hướng dẫn sử dụng các ví dụ trong thư mục
│
├── advanced_usage/
│   ├── example_advanced.go # Ví dụ nâng cao về cách sử dụng thư viện
│   ├── example_advanced.py # Ví dụ nâng cao bằng ngôn ngữ khác, nếu cần
│   └── README.md          # Hướng dẫn sử dụng các ví dụ nâng cao
│
└── README.md              # Tài liệu tổng quan về các ví dụ

```

## Thư mục init

Lưu trữ scripts hoặc tài nguyên liên quan đến khởi tạo hoặc cấu hình dự án. Có thể bao gồm script thiết lập môi trường phát triển, tạo db, hoặc các bước khởi tạo cần thiết khi bắt đầu làm việc với dự án.

```markdown
init/
├── database/
│   ├── create_schema.sql  # Script tạo cấu trúc cơ sở dữ liệu
│   ├── seed_data.sql      # Script chèn dữ liệu mẫu vào cơ sở dữ liệu
│   └── README.md          # Hướng dẫn sử dụng các script trong thư mục
│
├── environment/
│   ├── setup.sh           # Script thiết lập môi trường phát triển
│   ├── config.env         # Tệp cấu hình môi trường
│   └── README.md          # Hướng dẫn cấu hình môi trường
│
└── README.md              # Tài liệu tổng quan về các tài nguyên trong thư mục

```

## Thư mục githooks

Chứa các script được chạy tự động khi có các sự kiện git xảy ra như commit, push, merge code.

```markdown
githooks/
├── pre-commit
├── pre-push
├── post-merge
├── commit-msg
└── README.md

```

## Thư mục scripts

Lưu trữ các script hữu ích cho việc phát triển, triển khai, bảo trì. Bao gồm các công việc tự động hóa, quản lí hệ thống, task thường xuyên cần thực hiện trong quá trình phát triển và triển khai.

```markdown
scripts/
├── build/
│   ├── build.sh            # Script để xây dựng ứng dụng
│   └── README.md           # Hướng dẫn sử dụng các script trong thư mục build
│
├── deployment/
│   ├── deploy.sh           # Script để triển khai ứng dụng
│   └── README.md           # Hướng dẫn sử dụng các script trong thư mục deployment
│
├── maintenance/
│   ├── cleanup.sh          # Script để dọn dẹp các tệp tạm thời hoặc log
│   ├── backup.sh           # Script để sao lưu dữ liệu
│   └── README.md           # Hướng dẫn sử dụng các script trong thư mục maintenance
│
├── utilities/
│   ├── generate_keys.sh    # Script để tạo khóa hoặc mã bảo mật
│   ├── monitor.sh          # Script để giám sát hệ thống
│   └── README.md           # Hướng dẫn sử dụng các script trong thư mục utilities
│
└── README.md               # Tài liệu tổng quan về các script trong thư mục

```

## Thư mục tests

Lưu trữ các tài nguyên và script liên quan đến kiểm thử.

Đặt các bài kiểm tra tự động, công cụ kiểm thử, docs liên quan kiểm thử

```markdown
test/
├── unit/
│   ├── app_test.go         # Các bài kiểm tra đơn vị cho ứng dụng
│   └── README.md           # Hướng dẫn về các bài kiểm tra đơn vị
│
├── integration/
│   ├── api_integration_test.go  # Các bài kiểm tra tích hợp cho API
│   └── README.md               # Hướng dẫn về các bài kiểm tra tích hợp
│
├── e2e/
│   ├── end_to_end_test.go  # Các bài kiểm tra end-to-end cho toàn bộ ứng dụng
│   └── README.md           # Hướng dẫn về các bài kiểm tra end-to-end
│
├── mocks/
│   ├── mock_data.go        # Dữ liệu giả lập hoặc đối tượng giả để kiểm thử
│   └── README.md           # Hướng dẫn về cách sử dụng các mocks
│
└── README.md               # Tài liệu tổng quan về các tài nguyên kiểm thử trong thư mục

```

## Thư mục third_party

Chứa mã nguồn, thư viện hoặc tài nguyên bên ngoài mà dự án phụ thuộc.

```markdown
third_party/
├── library_a/
│   ├── src/
│   │   ├── lib_a.go
│   │   └── README.md
│   └── LICENSE.md
│
├── library_b/
│   ├── include/
│   │   ├── lib_b.h
│   │   └── README.md
│   ├── src/
│   │   ├── lib_b.cpp
│   │   └── README.md
│   └── LICENSE.md
│
└── README.md

```

## Thư mục tools

Chứa các công cụ hỗ trợ phát triển hoặc scripts liên quan đến quy trình phát triển của dự án

```markdown
tools/
├── build/
│   ├── build.sh            # Script xây dựng dự án
│   └── README.md           # Hướng dẫn về các công cụ xây dựng
│
├── lint/
│   ├── lint_config.json    # Cấu hình cho công cụ linting
│   └── README.md           # Hướng dẫn về cách sử dụng công cụ linting
│
├── deploy/
│   ├── deploy.sh           # Script triển khai
│   └── README.md           # Hướng dẫn về các công cụ triển khai
│
├── test/
│   ├── test_helpers.go     # Các công cụ hỗ trợ kiểm thử
│   └── README.md           # Hướng dẫn về các công cụ kiểm thử
│
└── README.md               # Tài liệu tổng quan về các công cụ trong thư mục

```

## Thư mục vendor

Lưu trữ các phụ thuộc của dự án, hoặc thư viện hoặc gói phần mềm bên ngoài mà chúng ta phụ thuộc vào.

Nhằm đảm bảo tất cả các thành phần cần thiết để xây dựng và chạy ứng dụng đều có sẵn trong dự án mà không phụ thuộc vào mạng

```markdown
vendor/
├── github.com/
│   ├── someuser/
│   │   ├── somepackage/
│   │   │   ├── file1.go
│   │   │   ├── file2.go
│   │   │   └── README.md
│   │   └── LICENSE.md
│   └── anotheruser/
│       └── anotherpackage/
│           ├── file1.go
│           └── README.md
│
├── golang.org/
│   └── x/
│       ├── module1/
│       │   ├── file1.go
│       │   └── README.md
│       └── LICENSE.md
│
└── README.md

```

## Thư mục web

Chứa tài nguyên liên quan đến giao diện người dùng của dự án

Tổ chức các thành phần liên quan đến giao diện và trình bày của ứng dụng web hoặc dịch vụ web.

```markdown
web/
├── app/
│   ├── main.go            # Tệp Go chính cho ứng dụng web (nếu là dự án Go)
│   ├── handlers.go        # Các trình xử lý yêu cầu HTTP
│   ├── routes.go          # Cấu hình các tuyến đường (routes)
│   └── README.md          # Tài liệu hướng dẫn về các thành phần trong thư mục app
│
├── static/
│   ├── css/
│   │   └── style.css      # Tệp CSS cho giao diện
│   ├── js/
│   │   └── script.js      # Tệp JavaScript cho các chức năng động
│   └── images/
│       ├── logo.png       # Hình ảnh logo
│       └── background.jpg # Hình ảnh nền
│
├── templates/
│   ├── layout.html        # Tệp mẫu layout chính
│   ├── index.html         # Tệp mẫu trang chính
│   └── README.md          # Tài liệu hướng dẫn về các tệp mẫu
│
└── README.md              # Tài liệu tổng quan về thư mục web

```