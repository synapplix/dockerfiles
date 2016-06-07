# Run yabe with linked mysql, and System environment varibales in application.conf
    docker create --volume /data --name yabe play1docker /bin/true
    docker cp $HOME/git/play yabe:/data
    docker cp $HOME/git/dockerfiles/play1docker/samples/yabe-with-db/application.conf yabe:/data/play/samples-and-tests/yabe/conf/application.conf
    docker run -it --rm --volumes-from yabe play1docker clean /data/play/samples-and-tests/yabe
    docker run -it --rm --volumes-from yabe play1docker deps /data/play/samples-and-tests/yabe
    docker run --name yabe-mysql --env MYSQL_DATABASE=yabe --env MYSQL_ROOT_PASSWORD=secret -d mysql:latest
    
    docker run --volumes-from yabe --name yabe-app --link yabe-mysql \
    -it --rm \
    --env PLAY_DB_URL=jdbc:mysql://yabe-mysql:3306/yabe \
    --env PLAY_DB_DRIVER=com.mysql.jdbc.Driver \
    --env PLAY_DB_USER=root \
    --env PLAY_DB_PASS=secret \
    play1docker run /data/play/samples-and-tests/yabe