# RAG-Pipeline

## 甚麼是RAG?

論文: [*Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*](https://arxiv.org/abs/2005.11401).  
[原著GitHub]https://github.com/mrdbourke/simple-local-rag/?tab=readme-ov-file#setup

RAG流程:

* **Retrieval** - 從給定的文件中提取Query的答案。  
`載入文件 -> chunking -> embedding -> 查詢 -> embed查詢 -> 比較查詢embeddings和chunks的embeddings`

* **Augmented** - 利用檢索到的資訊作為LLM的輸入。
* **Generation** - 從前面的Imput影響、優化LLM的輸出。

## 為什麼要RAG?

兩個主要改善：

<font color=#faf>**防止幻覺**</font> - LLM容易出現幻覺(hallucinations)，生成出看起來正確但其實是錯的內容。RAG可以幫助提供LLM帶有事實依據的參考。  
<font color=#faf>**自定義數據**</font> - LLM在語言方面能力強大，但往往缺乏**具體的知識**。RAG可以提供特定領域的數據，快速制定出<font color=#ffa>**特殊領域**</font>的知識庫，提供更多<font color=#ffa>可解釋性</font>。

RAG也可以是一種比在<font color=#ffa>**特定數據**</font>上微調LLM更快的解決方案。

### 為什麼Local? --> 隱私（自己的硬體）、成本、趨勢、（效率？）  

## 關鍵名詞

- **Token**  
- **Embedding** 
- **Embedding model**: 接收A個tokens的文本，轉成一個大小B的向量。 *嵌入模型可以與大型語言模型不同。*  
- **Similarity search/vector search(相似性檢索/向量檢索)**: 使用餘閒相似度(Cosine similarity)。相似文本相似度應該越高;不同文本應該相似度越低。  
- **LLM** 
- **Prompt**

## 建構項目

建構一個RAG的pipline，它可以和PDF進行對話，具體來說是一本開源的XX知識庫。

* 打開 PDF。
* 格式化PDF文本，為嵌入模型做好準備（過程稱為text splitting/chunking）。
* 將pdf的所有chunks嵌入並轉化為數字表示，稍後可以儲存這些數字。
* 建立一個使用向量搜索來根據查詢找到相關chunks的檢索系統。
* 創建一個包含檢索到的文本片段的prompt。
* 根據pdf的段落生成對查詢的回答

## 文件的embedding

所需物件
* PDF文件
* Embedding model

步驟:
1. 載入文件
2. text splitting/chunking
3. 嵌入embedding model.
4. 保存嵌入，日後使用
