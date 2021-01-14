
配置项目

# 拉取镜像并启动
docker-compose up -d

# 启动后，
第一次运行需要手动初始化mysql数据库
# 
⚠️注意: 只有第一次该这样做
docker-compose exec delos node scripts/init


# 部署成功后 
访问
http://localhost:3000 # 前端（可自定义端口号）
http://localhost:38080 # 后端

# 
如果访问不了可能是数据库没有链接上，关闭 rap 服务
docker-compose down
# 再重新运行
docker-compose up -d

# 如果 Sequelize 报错可能是数据库表发生了变化，
运行下面命令同步
docker-compose exec delos node scripts/updateSchema



镜像升级

Rap 
经常会进行 bugfix 和功能升级，
用 Docker 可以很方便地跟随主项目升级

# 拉取一下最新的镜像
docker-compose pull
# 暂停当前应用
docker-compose down
# 
重新构建并启动
docker-compose up -d --build
# 有时表结构会发生变化，执行下面命令同步
docker-compose exec delos node scripts/updateSchema
# 清空不被使用的虚悬镜像
docker image prune -f
