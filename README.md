# SỬ DỤNG PERMISSION SYTEM
- **Permission system là hệ thống quan trọng nhất của ABP về phần authorization.**
- **Một Permission là một simple policy được cấp hoặc cấm đối với user hoặc role cụ thể .**
- **Permission sẽ được link tới các function cụ thể của app để check khi user cố gắng truy cập vào chức năng đó.**

## 1. Định nghĩa ra Permissions
- **Để định nghĩa permissions trong hệ thống thì cần tạo một class kế thừa class PermissionDefinitionProvider nằm trong .\Acme.BookStore.Application.Contracts\Permissions\BookStorePermissionDefinitionProvider.cs**
	![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/3cb35f52-6d95-4fea-ac76-b003959e172f)

	![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/7171034b-228c-4466-8b28-3bd752d7331e)

	![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/66020955-4d8e-4330-a0cd-926498251ac3)

- **ABP Framework sẽ gọi hàm Define trong startup.**
	![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/8ecfa2da-d17f-4deb-957e-ae696d30238d)

- **Ở hình trên mình đã tạo một permission group tên là BookStore và định nghĩa ra 2 permissions chính vào trong group đấy và tạo ra 3 permissions con mới mỗi permission chính tương ứng với 3 chức năng CUD(tuy rằng tên group và permission nhận string nhưng khuyến khích dùng const string).**
	![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/6eaa934c-4777-46ab-bba6-c558d69f156f)

- **Đó là cấu hình tối thiểu. Ngoài ra cũng có thể cấu hình display names sử dụng hệ thống đa ngôn ngữ (.\Acme.BookStore.Domain.Shared\Localization\...) để thân thiện với người dùng.**
	
- **Sau khi cấu hình xong Permission thì sẽ có sẵn trên permission manager trên app.**

## 2. Managing permissions
- **Truy cập vào Administration/Identity Management/Roles page --> click Actiions Button --> click Permissions.**
	![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/a6a2259e-ff25-4f96-825d-7994a80fede8)

## 3. Checking Permissions
### 3.1 Bên phía server :
- **Sử dụng anotation  [Authorize] của IAuthorizationService như sau để check permission cho method(funtions).**
		![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/562a0590-ac1c-4e0a-aa60-8cfdd9ecaf80)

- **Trong trường hợp muốn check permission trong một block code(ví dụ: method) để lấy làm điều kiện thực thi thì phải inject IAuthorizationService và sử dụng như sau:**
		![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/7e635406-8e91-4d66-bd76-18f32bb44d74)


  		![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/06b014c4-d2f7-481c-bfcd-c81b66d840e3)


  - Trong trường hợp này:
	- IsGrantedAsync kiểm tra quyền hạn được cung cấp và trả về true nếu user hiện tại đã được cấp quyền hạn hiện tại. (Tiện cho việc custom logic trong các trường hợp phân quyền)
	- CheckAsync ném một ngoại lệ AbpAuthorizationException nếu user không có quyền thực hiện thao tác đó.(Được xử lý bởi ABP trả về response HTTP cho phía client)

### 3.2 Bên phía Client: 
- **Tùy thuộc vào Client khác nhau thì sẽ có các service khác nhau để check permission.**
- **Ví dụ ở MVC/Razor Pages thì sẽ sử dụng abp.auth của Javascript API để check:**
		![image](https://github.com/longdmhe161226/Permission_ABP/assets/100985816/2473a2b6-4dfa-4585-9b03-3edd082eaa4c)


