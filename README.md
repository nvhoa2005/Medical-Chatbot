# Medical Chatbot (RAG-based)

Một ứng dụng chatbot y tế đơn giản sử dụng Retrieval-Augmented Generation (RAG) để trả lời câu hỏi từ tài liệu y khoa. Ứng dụng kết hợp LangChain, Pinecone, HuggingFace Embeddings, OpenAI LLM và Flask để cung cấp giao diện web thân thiện.

# Điểm nổi bật:

1. Tải và xử lý tài liệu y khoa (PDF).
2. Chia nhỏ văn bản, nhúng embedding bằng HuggingFace (MiniLM-L6-v2).
3. Lưu trữ và truy vấn embedding với Pinecone Vector Database.
4. Trả lời câu hỏi bằng OpenAI GPT-4o dựa trên ngữ cảnh.
5. Giao diện chat trực quan với Flask + jQuery + Bootstrap.
6. Giao diện được thiết kế bằng CSS (UI giống ứng dụng chat).

# Cài đặt

1. Clone repo
2. Tạo môi trường ảo
python -m venv medicalchatbot
3. Cài đặt dependencies
pip install -r requirements.txt

# Cấu hình API Keys

Tạo file .env trong thư mục gốc:
    PINECONE_API_KEY=your_pinecone_api_key
    OPENAI_API_KEY=your_openai_api_key

# Tạo và lưu trữ Embeddings

Chạy lệnh sau để xử lý PDF và lưu embeddings vào Pinecone:
python store_index.py

# Chạy ứng dụng

Khởi động Flask server bằng lệnh sau:
python app.py

=> Mặc định chạy ở: http://localhost:8080

# Giao diện

Truy cập http://localhost:8080/
Giao diện chat hiển thị user message (bên phải) và bot reply (bên trái).
Hỗ trợ timestamp, avatar và kiểu chat UI.

# Thành phần chính

1. helpers.py

    load_pdf_file() → đọc file PDF từ thư mục.

    filter_to_minimal_docs() → tối giản metadata.

    text_split() → chia nhỏ văn bản thành chunks (500 tokens).

    download_hugging_face_embeddings() → tải model embedding MiniLM-L6-v2

2. store_index.py

    Xử lý PDF, tách văn bản, tạo embeddings.

    Kết nối Pinecone, tạo index medicalchatbot.

    Lưu chunks vào Pinecone để phục vụ truy vấn

3. app.py

Flask app với 2 route:

    / → render template chat.html.

    /get → nhận input, truy vấn RAG chain, trả về kết quả.

    Tích hợp ChatOpenAI với system prompt từ prompt.py

4. prompt.py
    Câu lệnh prompt kết hợp với dữ liệu từ file pdf (RAG)

5. chat.html + style.css

    Giao diện chat dùng Bootstrap 4, jQuery.

    Người dùng nhập câu hỏi → gửi AJAX → server trả câu trả lời → hiển thị trong UI

# Thử nghiệm

    Có notebook trials.ipynb để thử nghiệm pipeline RAG, embeddings và truy vấn.

# Ghi chú

    Model embedding: all-MiniLM-L6-v2 (384 dimensions).

    Pinecone index: medicalchatbot, metric = cosine.

    Có thể mở rộng để hỗ trợ nhiều tài liệu y khoa.

# Tác giả

    Tên: Nguyễn Văn Hòa
    Email: hoa049170@gmail.com