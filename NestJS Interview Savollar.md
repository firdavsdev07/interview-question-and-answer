# NestJS Interview Savollar

### 1. NestJS nima va nima uchun ishlatiladi?

👉 **NestJS** — Node.js ustida qurilgan **progressive framework**, u **TypeScript** asosida yozilgan.

- Express yoki Fastify ustida ishlaydi.
- Modular arxitekturaga ega.
- Enterprise level backend yaratishda juda qulay.

---

### 2. NestJS da module nima?

👉 **Module** — NestJS ilovasining asosiy bloklaridan biri.

- Har bir module o‘zining controller, service va providerlarini o‘z ichiga oladi.

📌 Misol:

```tsx
@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

---

### 3. Controller nima va qanday ishlatiladi?

👉 **Controller** — kiruvchi HTTP so‘rovlarni qabul qiladi va javob qaytaradi.

📌 Misol:

```tsx
@Controller('users')
export class UserController {
  @Get()
  findAll() {
    return ['Ali', 'Vali'];
  }
}

```

---

### 4. Service nima va nima uchun kerak?

👉 **Service** — biznes logika yoziladigan joy. Controller esa faqat request-response bilan ishlaydi.

📌 Misol:

```tsx
@Injectable()
export class UserService {
  getUsers() {
    return ['Ali', 'Vali'];
  }
}
```

---

### 5. Dependency Injection nima?

👉 **Dependency Injection (DI)** — boshqa class ichiga service yoki providerlarni avtomatik kiritish mexanizmi.

- NestJS DI’ni avtomatik qiladi.

📌 Misol:

```tsx
@Controller('users')
export class UserController {
  constructor(private readonly userService: UserService) {}

  @Get()
  findAll() {
    return this.userService.getUsers();
  }
}
```

---

### 6. Provider nima?

👉 **Provider** — NestJS’da service, repository yoki boshqa injectable obyektlar.

- `@Injectable()` decorator bilan belgilanadi.

---

### 7. Pipe nima va qachon ishlatiladi?

👉 **Pipe** — kelayotgan ma’lumotni **validatsiya qilish yoki transformatsiya qilish** uchun ishlatiladi.

📌 Misol:

```tsx
@Param('id', ParseIntPipe) id: number
```

---

### 8. Guard nima va nima uchun kerak?

👉 **Guard** — foydalanuvchi huquqlarini tekshiradi (masalan, auth).

📌 Misol:

```tsx
@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    return true; // yoki token check qilish
  }
}
```

---

### 9. Interceptor nima?

👉 **Interceptor** — request va response’ni o‘zgartirish yoki loglash uchun ishlatiladi.

- Masalan: response’ga qo‘shimcha data qo‘shish.

📌 Misol:

```tsx
@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler) {
    console.log('So‘rov kelmoqda...');
    return next.handle();
  }
}
```

---

### 10. Exception Filter nima va qanday ishlatiladi?

👉 **Exception Filter** — errorlarni boshqarish uchun ishlatiladi.

📌 Misol:

```tsx
@Catch(HttpException)
export class HttpErrorFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse();
    response.status(500).json({ message: exception.message });
  }
}
```