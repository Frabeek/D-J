from zipfile import ZipFile
from pathlib import Path

# 建立網站檔案內容
index_html_content = """<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>VR 動畫作品介紹</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header>
    <h1>VR 動畫作品｜《穿越之眼》</h1>
    <p>媒傳設計 · 2025 春季學期 · 作者：你的名字</p>
  </header>

  <main>
    <section class="preview">
      <img src="https://via.placeholder.com/600x340" alt="VR 動畫截圖" />
    </section>

    <section class="description">
      <h2>關於作品</h2>
      <p>
        《穿越之眼》是一部以「記憶與時間流動」為主題的 VR 動畫。觀眾將進入一個不穩定的時空空間，在片段中重新拼湊主角的意識與過去。
        製作技術包含 Blender + Unity，並使用 Meta Quest 作為展示平台。
      </p>
    </section>

    <section class="links">
      <h2>觀看連結</h2>
      <ul>
        <li><a href="https://youtu.be/你的影片ID" target="_blank">作品預告片</a></li>
        <li><a href="https://你的github.io/vr-project" target="_blank">GitHub 頁面</a></li>
        <li><a href="https://你的portfolio.com" target="_blank">個人作品集</a></li>
      </ul>
    </section>
  </main>

  <footer>
    <p>© 2025 你的名字 · VR動畫課期末作品</p>
  </footer>
</body>
</html>
"""

style_css_content = """body {
  font-family: "Noto Sans TC", sans-serif;
  background: linear-gradient(to bottom, #ffffff, #f0f4ff);
  margin: 0;
  color: #333;
  line-height: 1.6;
}

header {
  background-color: #2f4fcf;
  color: white;
  padding: 2em;
  text-align: center;
}

h1, h2 {
  margin-bottom: 0.5em;
}

main {
  padding: 2em;
  max-width: 800px;
  margin: auto;
}

.preview img {
  width: 100%;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.description, .links {
  margin-top: 2em;
}

.links ul {
  list-style-type: none;
  padding: 0;
}

.links a {
  color: #2f4fcf;
  text-decoration: none;
  font-weight: bold;
}

.links a:hover {
  text-decoration: underline;
}

footer {
  background-color: #f3f3f3;
  text-align: center;
  padding: 1em;
  font-size: 0.9em;
  margin-top: 3em;
}
"""

# 設定目錄與檔案
output_dir = Path("/mnt/data/vr-project")
output_dir.mkdir(parents=True, exist_ok=True)

(index_path := output_dir / "index.html").write_text(index_html_content, encoding="utf-8")
(style_path := output_dir / "style.css").write_text(style_css_content, encoding="utf-8")

# 壓縮成 zip 檔案
zip_path = Path("/mnt/data/vr-project.zip")
with ZipFile(zip_path, "w") as zipf:
    zipf.write(index_path, arcname="index.html")
    zipf.write(style_path, arcname="style.css")

zip_path
# D-J
