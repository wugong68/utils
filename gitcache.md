# utils
# 0. 进入项目路径
# 1. 清除本地当前的Git缓存
git rm -r --cached .

# 2. 应用.gitignore等本地配置文件重新建立Git索引
git add .

# 3. （可选）提交当前Git版本并备注说明
git commit -m 'update .gitignore'
