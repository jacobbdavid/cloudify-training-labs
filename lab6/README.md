# Lab 6: Deploying collectors and using the Grafana Dashboard

The purpose of this lab is to add monitoring to the Tomcat blueprint used in the previous lab.

### Step 1: Replace the placeholders

You need to replace all the occurrences of the placeholders (`REPLACE_THIS_WITH`) in `tomcat.yaml` and in the blueprint file to add monitoring to the blueprint.

### Step 2: Upload and install the blueprint

```bash
cfy blueprints upload -p LAB_ROOT/hello-tomcat/tomcat-blueprint.yaml -b hellotomcat-mon
cfy deployments create -b hellotomcat-mon -d hellotomcat-mon -i LAB_ROOT/hello-tomcat/tomcat.yaml
cfy executions start -d hellotomcat-mon -w install
```

### Step 3: Review monitoring in the UI

* In the web UI, go to the deployment screen.
* Click your deployment.
* Click the monitoring tab.
* Now you can see the grafana dashboard, with a few default metrics defined. This dashboard is dynamically created for every deployment when you click the monitoring tab.

### Step 4: �dd a new graph to the dashboard

Now let's add a new graph to the dashboard:

* Click the add a row button at the bottom right part of the screen 
* Click the right handle button, and then *Add panel* -> *Graph*
* Click the graph's title -> Edit
* Type `cpu` in the *Series* field. You should see a list of series names available in influx (these were pushed into influx by the CPU collector you installed in your blueprint. Choose one of them.
* Go to the *General* tab and give a meaningful title to your graph. You can also change the `span` attribute to control the width of the graph you just created (`12` being `100%` of the dashboard's width). Feel free to play around with the other tabs as well to define your graph.
* You can also control other aspects of the dashboard, e.g. the resolution, auto-refresh rate, etc.
* You can also export your dashboard to JSON by clicking *Save* -> *Export dashboard*.