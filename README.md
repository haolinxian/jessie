
import shutil
import os

# 创建部署文件夹
netlify_dir = '/mnt/agents/output/jessie-recipe-netlify'
os.makedirs(netlify_dir, exist_ok=True)

# 复制完整版HTML文件并重命名为index.html
shutil.copy('/mnt/agents/output/静怡bb的菜谱_完整版.html', os.path.join(netlify_dir, 'index.html'))

# 验证
files = os.listdir(netlify_dir)
print("Netlify部署文件夹内容:", files)
print(f"index.html 大小: {os.path.getsize(os.path.join(netlify_dir, 'index.html'))/1024:.1f} KB")

import zipfile

# 打包成zip文件，方便上传到Netlify
zip_path = '/mnt/agents/output/jessie-recipe.zip'
with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as zf:
    zf.write(os.path.join(netlify_dir, 'index.html'), 'index.html')

print(f"打包完成: {zip_path}")
print(f"ZIP文件大小: {os.path.getsize(zip_path)/1024:.1f} KB")
# jessie
