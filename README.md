# my-site
One-page static website for demo
# 로컬 폴더 준비
mkdir my-site && cd my-site
echo "<!DOCTYPE html><html><body>hello</body></html>" > index.html

# Git 초기화 및 첫 커밋
git init
git add index.html
git commit -m "first commit"

# 방금 만든 원격으로 연결(사용자명은 본인 것으로)
git remote add origin https://github.com/사용자명/my-site.git
git branch -M main
git push -u origin main
