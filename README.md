Bring up a cluster

edit the config to point to the file on your filesystem.

kind create cluster --config config

deploy chaoskube

kubectl create ns chaos

helm template . --namespace chaos | kubectl apply -n chaos -f-

In our values we have set an opt in annotation of chaos=true

Let's deploy an app.

kubectl apply -f kuard/

Then use vegeta and jaggr to see our results:

echo 'GET http://172.17.255.1:8080' | vegeta attack -rate 5000 -duration 10m | vegeta encode |  jaggr @count=rps hist\[100,200,300,400,500\]:code





