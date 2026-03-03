# 🍜 Vietnamese Food Image Search - Project Specification

**Đề tài:** Tìm kiếm ảnh món ăn Việt Nam  
**Môn học:** Một số vấn đề hiện đại về Khoa học dữ liệu  
**Thời gian:** 4 tuần  
**Mục tiêu:** Áp dụng Embeddings, Vector Database, và RAG

---

## 📋 MỤC TIÊU DỰ ÁN

### **Mục tiêu chính:**
1. ✅ Áp dụng **Image Embeddings** (Tuần 1.2)
2. ✅ Sử dụng **Vector Database** (Tuần 2.1)
3. ✅ Tích hợp **RAG** để giải thích món ăn (Tuần 2.2)
4. ✅ Xây dựng web app hoàn chỉnh

### **Khác biệt với lần trước:**
- ❌ Không train model (quá lâu)
- ✅ Dùng **pretrained model** để extract embeddings
- ✅ Dataset **nhỏ hơn** (100-200 images thay vì 25,000)
- ✅ Focus vào **Vector Search** và **RAG**
- ✅ Chạy được trên **CPU**

---

## 🎯 CHỨC NĂNG CHÍNH

### **Phase 1: Image Embeddings & Search (Tuần 1.2 + 2.1)**

#### **1.1. Upload & Extract Embeddings**
- **Input:** User upload ảnh món ăn
- **Process:**
  - Dùng pretrained model (EfficientNet/ResNet) extract embedding vector
  - Vector size: 512 hoặc 1024 dimensions
- **Output:** Embedding vector hiển thị trên UI

#### **1.2. Vector Database Storage**
- **Database:** FAISS hoặc ChromaDB
- **Data:**
  - 100-200 ảnh món ăn Việt Nam (30 classes)
  - Mỗi ảnh có: embedding vector + metadata (tên, vùng miền, mô tả)
- **Index:** Cosine similarity index

#### **1.3. Image Search**
- **Input:** User upload ảnh query
- **Process:**
  1. Extract embedding của ảnh query
  2. Tìm kiếm trong vector DB (cosine similarity)
  3. Trả về top 5 ảnh tương tự nhất
- **Output:**
  - 5 ảnh tương tự
  - Similarity score (%)
  - Thông tin món ăn

#### **1.4. Cosine Similarity Visualization**
- Hiển thị similarity score dạng progress bar
- So sánh vector của query vs results
- Visualize embeddings (optional: t-SNE)

---

### **Phase 2: RAG - Food Information (Tuần 2.2)**

#### **2.1. Food Knowledge Base**
- **Data:** 30 món ăn Việt Nam
- **Thông tin mỗi món:**
  - Tên (Việt + English)
  - Vùng miền (Bắc/Trung/Nam)
  - Nguyên liệu chính
  - Cách chế biến (tóm tắt)
  - Giá trị dinh dưỡng
  - Lịch sử/nguồn gốc
  - Địa điểm nổi tiếng

#### **2.2. Text Embeddings**
- Embedding mô tả món ăn bằng PhoBERT
- Lưu vào vector DB (text embeddings)

#### **2.3. RAG Q&A System**
- **Input:** User hỏi về món ăn
  - Ví dụ: "Phở có nguồn gốc từ đâu?"
  - "Món ăn nào ở miền Trung?"
  - "Cách làm bánh xèo như thế nào?"
- **Process:**
  1. Embedding câu hỏi
  2. Tìm trong knowledge base (retrieval)
  3. Đưa context + question vào LLM (Gemini/GPT)
  4. LLM sinh câu trả lời
- **Output:** Câu trả lời chi tiết + nguồn tham khảo

#### **2.4. Multi-modal Search**
- **Input:** Ảnh + Text query
- **Process:**
  - Combine image embedding + text embedding
  - Search trong cả 2 vector spaces
- **Output:** Kết quả tổng hợp

---

### **Phase 3: Advanced Features (Bonus)**

#### **3.1. Food Recognition**
- Nhận diện món ăn từ ảnh
- Hiển thị tên + confidence score

#### **3.2. Recipe Generation (RAG)**
- User upload ảnh món ăn
- LLM sinh công thức nấu ăn dựa trên knowledge base

#### **3.3. Nutrition Analysis**
- Phân tích dinh dưỡng món ăn
- Calories, protein, carbs, fat

#### **3.4. Regional Classification**
- Phân loại món ăn theo vùng miền
- Visualization: Map of Vietnam

#### **3.5. Recommendation System**
- Gợi ý món ăn tương tự
- Based on user preferences

#### **3.6. Batch Processing**
- Upload nhiều ảnh cùng lúc
- Batch embedding & search

---

## 🛠️ TECH STACK

### **Backend**
- **Framework:** Flask hoặc FastAPI
- **Image Embeddings:** 
  - EfficientNet-B0 (pretrained)
  - ResNet50 (pretrained)
  - CLIP (image-text embeddings)
- **Text Embeddings:**
  - PhoBERT (Vietnamese)
  - Sentence-BERT
- **Vector Database:**
  - FAISS (lightweight, local)
  - ChromaDB (with metadata)
  - Pinecone (cloud, optional)
- **LLM:**
  - Google Gemini API (free tier)
  - OpenAI GPT-3.5 (paid)
  - Hugging Face models (offline)
- **RAG Framework:**
  - LangChain
  - LlamaIndex

### **Frontend**
- **Framework:** HTML/CSS/JavaScript
- **UI Library:** Bootstrap hoặc Tailwind
- **Charts:** Chart.js
- **Image Upload:** Dropzone.js

### **Data Processing**
- **Image:** PIL, OpenCV
- **NLP:** Underthesea, PyVi
- **Vector Ops:** NumPy, SciPy

---

## 📊 DATASET

### **30VNFoods - Full Dataset** ✅
- **Source:** Kaggle - Vietnamese Foods Dataset
- **Link:** https://www.kaggle.com/datasets/quandang/vietnamese-foods
- **Size:** 4.2GB
- **Total Images:** 25,136 images
- **Classes:** 30 món ăn Việt Nam
- **Structure:**
  ```
  Data/Images/
  ├── Train/    (17,581 images) - Dùng để extract embeddings
  ├── Test/     (5,040 images)  - Dùng để test search
  └── Validate/ (2,515 images)  - Dùng để validate
  ```

### **30 Food Classes:**
1. Phở, 2. Bánh mì, 3. Bún bò Huế, 4. Gỏi cuốn, 5. Bánh xèo
6. Cơm tấm, 7. Cao lầu, 8. Mì Quảng, 9. Hủ tiếu, 10. Bún riêu
11. Bánh cuốn, 12. Bánh bèo, 13. Bánh khọt, 14. Bánh căn, 15. Nem chua
16. Cá kho tộ, 17. Canh chua, 18. Bún thịt nướng, 19. Bún đậu mắm tôm, 20. Xôi xéo
21. Bánh chưng, 22. Bánh tét, 23. Bánh pía, 24. Bánh tráng nướng, 25. Cháo lòng
26. Bún mắm, 27. Bánh canh, 28. Bánh đúc, 29. Bánh giò, 30. Bánh bột lọc

### **Approach: Extract Embeddings (NOT Training)**
- ❌ **Không train model** (quá lâu, 10-20 giờ)
- ✅ **Chỉ extract embeddings** từ pretrained EfficientNet/ResNet
- ✅ **Thời gian:** 2-3 giờ cho 25,136 images
- ✅ **Chạy trên CPU** (batch processing)
- ✅ **Lưu embeddings** vào file .npy (~500MB)
- ✅ **Build FAISS index** (~100MB)

### **Metadata Format:**
```json
{
  "pho": {
    "name_vi": "Phở",
    "name_en": "Pho",
    "region": "Bắc",
    "category": "Món chính",
    "ingredients": ["Bánh phở", "Thịt bò", "Hành", "Ngò"],
    "description": "Món ăn truyền thống của Việt Nam...",
    "calories": 350,
    "origin": "Hà Nội",
    "famous_places": ["Phở Thìn", "Phở Bát Đàn"]
  }
}
```

---

## 🎨 UI/UX DESIGN

### **Page 1: Home - Image Search**
```
┌─────────────────────────────────────────┐
│  🍜 Vietnamese Food Image Search        │
├─────────────────────────────────────────┤
│                                         │
│  [Upload Image or Drag & Drop]         │
│  ┌─────────────────────────────────┐   │
│  │     [Preview Image]             │   │
│  └─────────────────────────────────┘   │
│                                         │
│  [Search Similar Foods]                │
│                                         │
├─────────────────────────────────────────┤
│  📊 Results:                            │
│  ┌───────┐ ┌───────┐ ┌───────┐        │
│  │ Phở   │ │Bún bò │ │Bánh mì│        │
│  │ 95%   │ │ 87%   │ │ 82%   │        │
│  └───────┘ └───────┘ └───────┘        │
│                                         │
│  📝 Food Info: [RAG Generated]         │
└─────────────────────────────────────────┘
```

### **Page 2: Q&A with RAG**
```
┌─────────────────────────────────────────┐
│  💬 Ask about Vietnamese Food           │
├─────────────────────────────────────────┤
│                                         │
│  Question: [Text Input]                │
│  "Phở có nguồn gốc từ đâu?"            │
│                                         │
│  [Ask AI]                              │
│                                         │
├─────────────────────────────────────────┤
│  🤖 Answer:                             │
│  Phở là món ăn truyền thống của Việt   │
│  Nam, có nguồn gốc từ Hà Nội vào đầu   │
│  thế kỷ 20...                          │
│                                         │
│  📚 Sources:                            │
│  - Vietnamese Food Database             │
│  - Wikipedia                            │
└─────────────────────────────────────────┘
```

### **Page 3: Embeddings Visualization**
```
┌─────────────────────────────────────────┐
│  📊 Embeddings Visualization            │
├─────────────────────────────────────────┤
│                                         │
│  Query Image: [Image]                  │
│  Embedding Vector: [512 dimensions]    │
│  [0.23, -0.45, 0.67, ...]             │
│                                         │
│  Similarity Scores:                    │
│  ████████████████░░░░ 95% - Phở        │
│  ███████████████░░░░░ 87% - Bún bò     │
│  ██████████████░░░░░░ 82% - Bánh mì    │
│                                         │
│  [t-SNE Visualization]                 │
│  (Optional: 2D plot of embeddings)     │
└─────────────────────────────────────────┘
```

---

## 📁 PROJECT STRUCTURE

```
vietnamese-food-search/
├── app.py                      # Flask application
├── config.py                   # Configuration
├── requirements.txt            # Dependencies
│
├── models/
│   ├── image_embedder.py      # Image embedding model
│   ├── text_embedder.py       # Text embedding model
│   └── rag_system.py          # RAG implementation
│
├── database/
│   ├── vector_db.py           # Vector database interface
│   ├── faiss_index.bin        # FAISS index
│   └── metadata.json          # Food metadata
│
├── data/
│   ├── images/                # Food images (100-200)
│   │   ├── pho/
│   │   ├── banh_mi/
│   │   └── ...
│   └── knowledge_base/        # Text data for RAG
│       └── food_info.json
│
├── static/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── main.js
│   └── uploads/               # User uploaded images
│
├── templates/
│   ├── base.html
│   ├── index.html             # Image search
│   ├── qa.html                # Q&A with RAG
│   └── visualization.html     # Embeddings viz
│
├── utils/
│   ├── image_processing.py    # Image preprocessing
│   ├── similarity.py          # Cosine similarity
│   └── visualization.py       # t-SNE, plots
│
└── notebooks/
    ├── 1_embeddings_demo.ipynb      # Tuần 1.1
    ├── 2_image_embeddings.ipynb     # Tuần 1.2
    ├── 3_vector_db.ipynb            # Tuần 2.1
    └── 4_rag_system.ipynb           # Tuần 2.2
```

---

## 🚀 IMPLEMENTATION PLAN

### **Week 1: Embeddings (Tuần 1.1 + 1.2)**

#### **Day 1-2: Setup & Pretrained Model**
- [ ] Setup project structure
- [ ] Install dependencies
- [ ] Download 30VNFoods dataset (4.2GB)
- [ ] Load pretrained EfficientNet-B0
- [ ] Test embedding extraction với 10 images

#### **Day 3-5: Extract ALL Embeddings**
- [ ] Implement batch embedding extraction
- [ ] Extract embeddings cho 17,581 train images
- [ ] Extract embeddings cho 5,040 test images
- [ ] Extract embeddings cho 2,515 validate images
- [ ] **Total time:** ~2-3 giờ trên CPU
- [ ] Save embeddings to .npy files (~500MB)

#### **Day 6-7: Vector Operations & Visualization**
- [ ] Implement cosine similarity
- [ ] Test với các cặp images
- [ ] Visualize similarity scores
- [ ] Create Jupyter notebook demo
- [ ] Test search với query images

---

### **Week 2: Vector DB & Search (Tuần 2.1)**

#### **Day 1-2: Vector Database**
- [ ] Install FAISS
- [ ] Build FAISS index from embeddings
- [ ] Implement search function
- [ ] Test search với query images

#### **Day 3-4: Web Application**
- [ ] Create Flask app
- [ ] Implement upload endpoint
- [ ] Implement search endpoint
- [ ] Build frontend UI

#### **Day 5-7: Testing & Optimization**
- [ ] Test search accuracy
- [ ] Optimize search speed
- [ ] Add error handling
- [ ] Polish UI/UX

---

### **Week 3: RAG System (Tuần 2.2)**

#### **Day 1-2: Knowledge Base**
- [ ] Create food information database
- [ ] Extract text embeddings (PhoBERT)
- [ ] Store in vector DB

#### **Day 3-4: LLM Integration**
- [ ] Setup Gemini API
- [ ] Implement RAG pipeline
- [ ] Test Q&A system

#### **Day 5-7: Multi-modal Search**
- [ ] Combine image + text search
- [ ] Implement recipe generation
- [ ] Add food information display

---

### **Week 4: Advanced Features & Demo**

#### **Day 1-3: Advanced Features**
- [ ] Food recognition
- [ ] Nutrition analysis
- [ ] Regional classification
- [ ] Recommendation system

#### **Day 4-5: Documentation**
- [ ] Write README
- [ ] Create user guide
- [ ] Document API endpoints
- [ ] Write technical report

#### **Day 6-7: Demo & Presentation**
- [ ] Create demo video
- [ ] Prepare slides
- [ ] Test all features
- [ ] Deploy (optional)

---

## 📝 DELIVERABLES

### **Code**
- [ ] Complete source code
- [ ] Requirements.txt
- [ ] Configuration files
- [ ] Database files

### **Documentation**
- [ ] README.md
- [ ] Technical report (PDF)
- [ ] API documentation
- [ ] User guide

### **Demo**
- [ ] Working web application
- [ ] Demo video (3-5 minutes)
- [ ] Presentation slides
- [ ] Jupyter notebooks

### **Report Sections**
1. **Giới thiệu**
   - Bài toán
   - Mục tiêu
   - Phạm vi

2. **Cơ sở lý thuyết**
   - Image embeddings
   - Vector databases
   - RAG
   - Cosine similarity

3. **Thiết kế hệ thống**
   - Kiến trúc
   - Tech stack
   - Database schema

4. **Thực nghiệm**
   - Dataset
   - Embeddings extraction
   - Search performance
   - RAG evaluation

5. **Kết quả**
   - Accuracy metrics
   - Search speed
   - User interface
   - Demo screenshots

6. **Kết luận**
   - Thành tựu
   - Hạn chế
   - Hướng phát triển

---

## 🎯 SUCCESS CRITERIA

### **Functional Requirements**
- ✅ Upload ảnh và search được món ăn tương tự
- ✅ Hiển thị top 5 kết quả với similarity score
- ✅ Q&A system với RAG hoạt động
- ✅ Hiển thị thông tin món ăn chi tiết
- ✅ UI đẹp, dễ sử dụng

### **Technical Requirements**
- ✅ Embeddings extraction < 2 seconds per image
- ✅ Total extraction time: 2-3 hours for 25,136 images
- ✅ Search time < 1 second (FAISS index)
- ✅ RAG response < 5 seconds
- ✅ Support 25,000+ images
- ✅ Chạy được trên CPU (batch processing)

### **Documentation Requirements**
- ✅ Code có comments đầy đủ
- ✅ README hướng dẫn cài đặt
- ✅ Technical report đầy đủ
- ✅ Demo video rõ ràng

---

## 💡 TIPS & BEST PRACTICES

### **Embeddings**
- Dùng pretrained models (không train lại)
- Normalize vectors trước khi lưu
- Cache embeddings để tăng tốc

### **Vector Database**
- FAISS cho local, nhẹ
- ChromaDB nếu cần metadata filtering
- Index type: IVF hoặc HNSW

### **RAG**
- Keep context ngắn gọn
- Use prompt engineering
- Cache LLM responses

### **Performance**
- Batch processing cho embeddings
- Use GPU nếu có (optional)
- Compress images trước khi upload

### **UI/UX**
- Show loading states
- Display progress bars
- Handle errors gracefully
- Mobile responsive

---

## 🐛 COMMON ISSUES & SOLUTIONS

### **Issue 1: Out of Memory**
**Solution:** 
- Giảm batch size
- Resize images nhỏ hơn
- Use float16 instead of float32

### **Issue 2: Slow Search**
**Solution:**
- Use FAISS GPU (if available)
- Reduce vector dimensions (PCA)
- Use approximate search

### **Issue 3: Poor Search Results**
**Solution:**
- Use better pretrained model (CLIP)
- Increase dataset size
- Fine-tune embeddings

### **Issue 4: RAG Hallucination**
**Solution:**
- Improve retrieval quality
- Add more context
- Use better prompts
- Verify with sources

---

## 📚 LEARNING RESOURCES

### **Embeddings**
- [Sentence Transformers](https://www.sbert.net/)
- [CLIP by OpenAI](https://github.com/openai/CLIP)
- [Image Embeddings Tutorial](https://www.tensorflow.org/tutorials/images/transfer_learning)

### **Vector Databases**
- [FAISS Documentation](https://github.com/facebookresearch/faiss)
- [ChromaDB Guide](https://docs.trychroma.com/)
- [Vector DB Comparison](https://www.pinecone.io/learn/vector-database/)

### **RAG**
- [LangChain RAG Tutorial](https://python.langchain.com/docs/use_cases/question_answering/)
- [RAG Paper](https://arxiv.org/abs/2005.11401)
- [Building RAG Systems](https://www.youtube.com/watch?v=z1OfI_NOvgI)

### **Vietnamese NLP**
- [PhoBERT](https://github.com/VinAIResearch/PhoBERT)
- [Underthesea](https://github.com/undertheseanlp/underthesea)

---

## 🎉 CONCLUSION

Dự án này sẽ giúp bạn:
- ✅ Hiểu sâu về embeddings (image + text)
- ✅ Thực hành với vector databases
- ✅ Xây dựng RAG system hoàn chỉnh
- ✅ Áp dụng LLM vào thực tế
- ✅ Có portfolio project đẹp

**Estimated Time:** 4 weeks  
**Difficulty:** Medium  
**Fun Factor:** High! 🚀

---

**Ready to start? Let's build it! 🍜**
