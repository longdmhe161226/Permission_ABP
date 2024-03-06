# SỬ DỤNG PERMISSION SYTEM
- **Permission system là hệ thống quan trọng nhất của ABP về phần authorization.**
- **Một Permission là một simple policy được cấp hoặc cấm đối với user hoặc role cụ thể .**
- **Permission sẽ được link tới các function cụ thể của app để check khi user cố gắng truy cập vào chức năng đó.**

## 1. Định nghĩa ra Permissions
- **Để định nghĩa permissions trong hệ thống thì cần tạo một class kế thừa class PermissionDefinitionProvider nằm trong .\Acme.BookStore.Application.Contracts\Permissions\BookStorePermissionDefinitionProvider.cs**
	***Insert hình***
- **ABP Framework sẽ gọi hàm Define trong startup.**
	***insert hình Defined method***
- **Ở hình trên mình đã tạo một permission group tên là BookStore và định nghĩa ra 2 permissions chính vào trong group đấy và tạo ra 3 permissions con mới mỗi permission chính tương ứng với 3 chức năng CUD(tuy rằng tên group và permission nhận string nhưng khuyến khích dùng const string).**
	***Insert hình LocalizableString method***
- **Đó là cấu hình tối thiểu. Ngoài ra cũng có thể cấu hình display names sử dụng hệ thống đa ngôn ngữ (.\Acme.BookStore.Domain.Shared\Localization\...) để thân thiện với người dùng.**

- **Sau khi cấu hình xong Permission thì sẽ có sẵn trên permission manager trên app.**

## 2. Managing permissions
- **Truy cập vào Administration/Identity Management/Roles page --> click Actiions Button --> click Permissions.**
	***Inser hình manager permissions***

## 3. Checking Permissions
### 3.1 Bên phía server :
- **Sử dụng anotation  [Authorize] của IAuthorizationService như sau để check permission cho method(funtions).**
		***Insert hình***
- **Trong trường hợp muốn check permission trong một block code(ví dụ: method) để lấy làm điều kiện thực thi thì phải inject IAuthorizationService và sử dụng như sau:**
		***Insert hình***
  - Trong trường hợp này:
      - IsGrantedAsync kiểm tra quyền hạn được cung cấp và trả về true nếu user hiện tại đã được cấp quyền hạn hiện tại. (Tiện cho việc custom logic trong các trường hợp phân quyền)
	    - CheckAsync ném một ngoại lệ AbpAuthorizationException nếu user không có quyền thực hiện thao tác đó.(Được xử lý bởi ABP trả về response HTTP cho phía client)

### 3.2 Bên phía Client: 
- **Tùy thuộc vào Client khác nhau thì sẽ có các service khác nhau để check permission.**
- **Ví dụ ở MVC/Razor Pages thì sẽ sử dụng abp.auth của Javascript API để check:**
		***Insert hình***

