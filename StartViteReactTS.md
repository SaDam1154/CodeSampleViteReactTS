Cấu trúc thư mục ReactJs Vite
Dưới đây là cấu trúc thư mục hoàn chỉnh của dự án ReactJs Typescript Vite ESLint Prettier

txt
📦react-app
┣ 📂dist
┣ 📂public
┃ ┗ 📜vite.svg
┣ 📂src
┃ ┣ 📂assets
┃ ┃ ┗ 📜react.svg
┃ ┣ 📜App.css
┃ ┣ 📜App.tsx
┃ ┣ 📜index.css
┃ ┣ 📜main.tsx
┃ ┗ 📜vite-env.d.ts
┣ 📜.editorconfig
┣ 📜.eslintignore
┣ 📜.eslintrc.cjs
┣ 📜.gitignore
┣ 📜.prettierignore
┣ 📜.prettierrc
┣ 📜index.html
┣ 📜package-lock.json
┣ 📜package.json
┣ 📜tsconfig.json
┣ 📜tsconfig.node.json
┗ 📜vite.config.ts
Thư mục dist: Thư mục chứa các file build
Thư mục public: Chứa file index.html và các file liên quan như favicon.ico, robots.txt,...
Thư mục src: Chứa mã nguồn chính của chúng ta
Thư mục src/assets: Chứa media, css (file App.css và index.css ở trên mình để nguyên xi khi mới tạo, anh em có thể đưa vào assets/styles cho gọn nhé), fonts
Còn lại những file config sẽ được mình giới thiệu ở những phần dưới
🥇Bước 1 - Khởi tạo dự án Vite
Vite yêu cầu Node version 14.18+, 16+ để có thể hoạt động ổn định. Tuy nhiên một số template yêu cầu version cao hơn, vậy nên nếu nó warning thì anh em update nodejs lên version cao hơn nhé.

Các bạn có thể dùng npm hoặc yarn hoặc pnpm đều được, ở đây mình dùng npm cho đơn giản.

Với npm

bash
npm create vite@latest
Với Yarn

bash
yarn create vite
Với PNPM

bash
pnpm create vite
Sau khi chạy thì nó sẽ yêu cầu nhập tên dự án

bash
Need to install the following packages:
create-vite@4.1.0
Ok to proceed? (y) y
✔ Project name: … react-app
Tiếp theo là chọn Framework

bash
✔ Select a framework: › React
Chọn template, ở đây mình chọn TypeScript + SWC, SWC sẽ thay thế Babel cho việc biên dịch code Typescript/Javascript. SWC có tốc độ nhanh hơn 20 lần khi so với Babel

bash
✔ Select a variant: › TypeScript + SWC
Tiếp theo là thư mục vừa được Vite tạo

bash
cd react-app
Cài đặt các package

bash
npm i
🥇Bước 2 - Cài các package liên quan ESLint và Prettier
Sau khi xong bước 1 rồi thì mặc định Vite đã giúp chúng ta cấu hình cơ bản cho ESLint và TypeScript rồi, nhưng để tiện hơn cho việc code thì chúng ta sẽ cài thêm 1 số package nữa.

Chạy câu lệnh sau

bash
npm i prettier eslint-config-prettier eslint-plugin-prettier -D
Đây là những thứ chúng ta cài

prettier: code formatter chính

eslint-config-prettier: Bộ config ESLint để vô hiệu hóa các rule của ESLint mà xung đột với Prettier.

eslint-plugin-prettier: Dùng thêm 1 số rule Prettier cho ESLint

🥇Bước 3 - Config ESlint để chuẩn hóa code
Mở file eslint.config.js lên

Thêm đoạn giá trị này vào mảng ignores, mục đích là mình không muốn ESLint check file vite.config.ts

ts
'vite.config.ts'
Các bạn import cái này vào đầu file eslint.config.js

ts
import eslintPluginPrettier from 'eslint-plugin-prettier'
Thêm đoạn code sau vào object plugins

ts
prettier: eslintPluginPrettier
Thêm đoạn code sau vào object rules để thêm các rule của Prettier

ts
'prettier/prettier': [
'warn',
{
arrowParens: 'always',
semi: false,
trailingComma: 'none',
tabWidth: 2,
endOfLine: 'auto',
useTabs: false,
singleQuote: true,
printWidth: 120,
jsxSingleQuote: true
}
]
🥇Bước 4 - Config Prettier để format code
Tạo file .prettierrc trong thư trong thư mục root với nội dung dưới đây

json
{
"arrowParens": "always",
"semi": false,
"trailingComma": "none",
"tabWidth": 2,
"endOfLine": "auto",
"useTabs": false,
"singleQuote": true,
"printWidth": 120,
"jsxSingleQuote": true
}
Mục đích là cấu hình prettier. Anh em nên cài Extension Prettier - Code formatter cho VS Code để nó hiểu nhé.

Tiếp theo Tạo file .prettierignore ở thư mục root

Mục đích là Prettier bỏ qua các file không cần thiết

ignore
node_modules/
dist/
🥇Bước 5 - Config editor để chuẩn hóa cấu hình editor
Tạo file .editorconfig ở thư mục root

Mục đích là cấu hình các config đồng bộ các editor với nhau nếu dự án có nhiều người tham gia.

Để VS Code hiểu được file này thì anh em cài Extension là EditorConfig for VS Code nhé

editorconfig
[*]
indent_size = 2
indent_style = space
🥇Bước 6 - Cấu hính alias cho tsconfig.json
Việc thêm alias vào file tsconfig.json sẽ giúp VS Code hiểu mà tự động import giúp chúng ta. Lưu ý cái này chỉ giúp

Thêm đoạn này vào compilerOptions trong file tsconfig.json

json
"baseUrl": ".",
"paths": {
"~/_": ["src/_"]
}
file tsconfig.json của bạn sẽ có kiểu như dưới đây

json
{
"files": [],
"references": [{ "path": "./tsconfig.app.json" }, { "path": "./tsconfig.node.json" }],
"compilerOptions": {
"baseUrl": ".",
"paths": {
"~/_": ["src/_"]
}
}
}
Ý nghĩa của đoạn này là ta có thể import Login from '~/pages/Login' thay vì import Login from '../../pages/Login'. Ngắn gọn và dễ nhìn hơn nhiều!

🥇Bước 7 - Cấu hình alias cho vite vite.config.ts
Cài package @types/node để sử dụng node js trong file ts không bị lỗi

bash
npm i @types/node -D
Cấu hình alias và enable source map ở file vite.config.ts

ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react-swc'
import path from 'path'

// https://vitejs.dev/config/
export default defineConfig({
plugins: [react()],
server: {
port: 3000
},
css: {
devSourcemap: true
},
resolve: {
alias: {
'~': path.resolve(\_\_dirname, './src')
}
}
})
🥇Bước 8 - Cập nhật script cho package.json
Mở file package.json lên, thêm đoạn script dưới vào

json
"scripts": {
//...
"lint:fix": "eslint . --fix",
"prettier": "prettier --check \"src/**/(_.tsx|_.ts|_.css|_.scss)\"",
"prettier:fix": "prettier --write \"src/**/(_.tsx|_.ts|_.css|_.scss)\""
}
🥇Câu lệnh để chạy dự án
Đến đây là xong rồi đó, để chạy trong môi trường dev thì chúng ta sẽ chạy bằng câu lệnh npm run dev.

Nếu muốn build thì npm run build

Ngoài ra còn có một số câu lệnh như

Preview kết quả build bằng câu lệnh npm run preview
Kiểm tra dự án có bị lỗi gì liên quan ESLint không: npm run lint
Tự động fix các lỗi liên quan ESLint (không phải cái gì cũng fix được, nhưng fix cũng nhiều): npm run lint:fix
Kiểm tra dự án có bị lỗi gì liên quan Prettier không: npm run prettier
Tự động fix các lỗi liên quan Prettier: npm run prettier:fix
Chúc các bạn thành công nhen!
