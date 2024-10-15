# RESTful API 最佳实践 (Angular 示例代码)

在这个部分，我们将展示如何使用 **Angular** 来与RESTful API进行交互。通过HttpClient模块，我们可以在Angular中发送GET、POST、PUT、DELETE等请求，并处理API返回的状态码和数据。

#### 1. **使用HTTP动词**
   在Angular中，可以使用`HttpClient`来进行各种HTTP请求操作，如GET、POST、PUT、DELETE等。以下是每种HTTP动词的使用示例：

   **Angular 代码示例**:
   ```typescript
   import { HttpClient } from '@angular/common/http';
   import { Injectable } from '@angular/core';
   import { Observable } from 'rxjs';

   @Injectable({
     providedIn: 'root'
   })
   export class UserService {
     private baseUrl = 'https://api.example.com/v1/users';

     constructor(private http: HttpClient) {}

     // GET: 获取资源
     getUser(id: number): Observable<any> {
       return this.http.get(`${this.baseUrl}/${id}`);
     }

     // POST: 创建资源
     createUser(user: any): Observable<any> {
       return this.http.post(this.baseUrl, user);
     }

     // PUT: 更新资源（完整替换）
     updateUser(id: number, user: any): Observable<any> {
       return this.http.put(`${this.baseUrl}/${id}`, user);
     }

     // PATCH: 部分更新资源
     partialUpdateUser(id: number, user: any): Observable<any> {
       return this.http.patch(`${this.baseUrl}/${id}`, user);
     }

     // DELETE: 删除资源
     deleteUser(id: number): Observable<any> {
       return this.http.delete(`${this.baseUrl}/${id}`);
     }
   }
   ```

   **比较表**：

   | HTTP动词 | 用途                   | Angular 路由调用                         | 幂等性  |
   |----------|------------------------|-----------------------------------------|---------|
   | GET      | 获取资源                | `getUser(id: number)`                   | 是      |
   | POST     | 创建资源                | `createUser(user: any)`                 | 否      |
   | PUT      | 更新资源（完整替换）    | `updateUser(id: number, user: any)`     | 是      |
   | PATCH    | 部分更新资源            | `partialUpdateUser(id: number, user: any)` | 是  |
   | DELETE   | 删除资源                | `deleteUser(id: number)`                | 是      |

#### 2. **使用有意义的URL**
   Angular中的URL应该清晰、简洁，反映出操作的资源类型。通过定义服务中的基础URL，简化代码。

   **Angular 代码示例**:
   ```typescript
   getUsers(): Observable<any[]> {
     return this.http.get<any[]>(this.baseUrl);
   }
   ```

   **示例**:
   - 错误: `/getAllUsers`
   - 正确: `/v1/users`

#### 3. **状态码的使用**
   Angular的`HttpClient`模块会自动处理状态码，并且可以通过拦截器或在调用处处理不同的HTTP状态码。

   **Angular 代码示例**:
   ```typescript
   import { HttpErrorResponse } from '@angular/common/http';

   getUser(id: number): Observable<any> {
     return this.http.get(`${this.baseUrl}/${id}`).pipe(
       catchError(this.handleError)
     );
   }

   private handleError(error: HttpErrorResponse): Observable<never> {
     let errorMessage = '';
     if (error.status === 404) {
       errorMessage = 'User not found';
     } else if (error.status === 500) {
       errorMessage = 'Internal server error';
     }
     return throwError(errorMessage);
   }
   ```

   **比较表**：

   | 状态码 | 描述                     | Angular 代码示例                         |
   |--------|--------------------------|----------------------------------------|
   | 200    | OK                       | `this.http.get()`                      |
   | 201    | Created                  | `this.http.post()`                     |
   | 204    | No Content               | `this.http.delete()`                   |
   | 400    | Bad Request              | `catchError(this.handleError)`          |
   | 401    | Unauthorized             | `catchError(this.handleError)`          |
   | 403    | Forbidden                | `catchError(this.handleError)`          |
   | 404    | Not Found                | `catchError(this.handleError)`          |
   | 500    | Internal Server Error    | `catchError(this.handleError)`          |

#### 4. **版本控制**
   在Angular中，我们可以通过定义基础URL来处理不同的API版本。在下面的例子中，我们将展示如何在API请求中包含版本号。

   **Angular 代码示例**:
   ```typescript
   private baseUrlV1 = 'https://api.example.com/v1/users';
   private baseUrlV2 = 'https://api.example.com/v2/users';

   getUserV1(id: number): Observable<any> {
     return this.http.get(`${this.baseUrlV1}/${id}`);
   }

   getUserV2(id: number): Observable<any> {
     return this.http.get(`${this.baseUrlV2}/${id}`);
   }
   ```

   **示例**:
   - `GET /v1/users/{id}`: 获取V1版本的用户信息
   - `GET /v2/users/{id}`: 获取V2版本的用户信息

#### 5. **分页、过滤和排序**
   Angular可以通过在请求参数中加入分页、过滤和排序信息，来与API进行交互。

   **Angular 代码示例**:
   ```typescript
   getUsers(page: number = 1, size: number = 10, sort: string = 'id'): Observable<any[]> {
     return this.http.get<any[]>(`${this.baseUrl}?page=${page}&size=${size}&sort=${sort}`);
   }
   ```

   **示例**:
   - 分页：`GET /v1/users?page=2&size=10`
   - 排序：`GET /v1/users?sort=name`

#### 6. **幂等性**
   Angular中的PUT和DELETE请求通常是幂等的，可以多次调用而不会改变最终结果。

   **Angular 代码示例**:
   ```typescript
   updateUser(id: number, user: any): Observable<any> {
     return this.http.put(`${this.baseUrl}/${id}`, user);
   }

   deleteUser(id: number): Observable<any> {
     return this.http.delete(`${this.baseUrl}/${id}`);
   }
   ```

#### 7. **安全性**
   使用`HttpInterceptor`来添加身份验证Token到HTTP请求头，确保每个API调用都包含认证信息。

   **Angular 代码示例**:
   ```typescript
   import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
   import { Injectable } from '@angular/core';
   import { Observable } from 'rxjs';

   @Injectable()
   export class AuthInterceptor implements HttpInterceptor {
     intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
       const token = 'your-token-here';
       const clonedReq = req.clone({
         headers: req.headers.set('Authorization', `Bearer ${token}`)
       });
       return next.handle(clonedReq);
     }
   }
   ```

   **示例**:
   - 使用Token身份验证：
     ```typescript
     this.http.get('/v1/users/me').subscribe();
     ```

#### 8. **错误处理**
   Angular提供了`HttpInterceptor`来全局处理错误，或使用`catchError`处理单个请求中的错误。

   **Angular 代码示例**:
   ```typescript
   getUser(id: number): Observable<any> {
     return this.http.get(`${this.baseUrl}/${id}`).pipe(
       catchError(this.handleError)
     );
   }

   private handleError(error: HttpErrorResponse): Observable<never> {
     let errorMessage = 'An error occurred';
     if (error.status === 404) {
       errorMessage = 'User not found';
     } else if (error.status === 500) {
       errorMessage = 'Internal server error';
     }
     return throwError(errorMessage);
   }
   ```

#### 9. **文档**
   Angular没有生成API文档的功能，但可以使用Swagger等工具生成后端的API文档，以便前端开发者参考。开发者可以访问 `/docs` 或 `/swagger` 查看API文档。

---

### 总结

通过Angular中的HttpClient模块，我们可以轻松与RESTful API进行交互，结合拦截器实现安全性、错误处理等最佳实践。结合分页、过滤、排序、幂等性和状态码的处理，Angular为构建高效、安全的API提供了强大的支持。
