PREDICTION IO WITH RECCOMENDATION TEMPATE
SETTING UP PREDICTIONIO FROM GIT
1.	Clone Prediction and Dependencies Configuration Docker
2.	  YML Files from the following repository: 
https://github.com/jawmeschege/PredictionIo.git
3.	Build Docker Image :  docker build -t predictionio/pio pio
Alternatively you can:
1.	 pull the image directly from docket hub using: 
docker pull predictionio/pio

2.	Start the service using:
docker-compose -f docker-compose.yml \
    -f pgsql/docker-compose.base.yml \
    -f pgsql/docker-compose.meta.yml \
    -f pgsql/docker-compose.event.yml \
    -f pgsql/docker-compose.model.yml \
    up

3.	Verify the service:
$ export PATH=`pwd`/bin:$PATH
$ pio-docker status

4.	Start the engine using  pio eventserver & or pio-start-all
5.	Check the engine by running  pio status
SETTING UP THE RECCOMENDATION ENGINE
1.	Bash inside the container shell
2.	Go to any directory like where you want to set it up i.e templates
3.	Create a new Engine from an Engine Template
git clone https://github.com/apache/predictionio-template-recommender.git MyRecommendation
cd MyRecommendation

4.	Create a new App using :  pio app new MyApp1
5.	To list the app's use pio app list
6.	Take note of the Access Key given
7.	Import sample data:
a.	Pip install predictionio
curl https://raw.githubusercontent.com/apache/spark/master/data/mllib/sample_movielens_data.txt --create-dirs -o data/sample_movielens_data.txt

python data/import_eventserver.py --access_key $ACCESS_KEY
8.	Deploy the engine as a service
a.	curl -L -o $HOME/.sbt/launchers/0.13.8/sbt-launch.jar http://repo.typesafe.com/typesafe/ivy-releases/org.scala-sbt/sbt-launch/0.13.8/sbt-launch.jar   to download sbt on that lauhcers directory
b.	echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
c.	apt-get update
d.	apt-get install sbt
e.	Build the engine using pio build –verbose 
f.	Train the Predictive model using pio train
g.	Deploy the engine using pio deploy  -- <port>
h.	Access your deployed engine from http://<your_IP_ADDRESS:PORT>


POSTING DATA AND QUERYING THE MODEL

