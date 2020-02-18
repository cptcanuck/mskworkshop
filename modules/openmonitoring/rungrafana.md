# Running Grafana

We are going to use Grafana as a tool to visualize and Dashboard KSK cluster and topic metrics that are being collected by Prometheus.  Prometheus offers a nice ui for reviewing single metrics, but if you're going to run MSK in production, you'll want nice dashboards.

We will be using Docker to run Grafana on your Kafka Jumpbox - this should keep things nice and simple!


1. Connect to your Kafka Jumpbox as ec2-user

1. Start Grafana in docker:

`docker run -d -p 3000:3000 --name=grafana -e "GF_INSTALL_PLUGINS=grafana-clock-panel" grafana/grafana

1. Connect to your Kafka Jumpboxes public IP Address on port 3000.  An example would be `https://1.2.3.4:3000`.  You should see a Grafana login screen

1. Login with username "admin", password "admin"

1. Feel free to change the password to whatever you feel like when prompted to change it, or hit `Skip`

We now need to add a Data Source to pull in in Time Series data from Prometheus

1. Click on `Add Data Source`

1. Hover over `Prometheus` then click the `Select` button

1. Fill out the configuration:

**Note**: You are going to need the public IP for your Kafka Jumpbox for this

        URL: *http://[jumpox public IP]:9000*
        Access: Server (default)

Click **Save and Test** - the results should come back Green - `Data Source is working`.  If you get an error, check that your security groups were setup properly in the [Preparation](/modules/openmonitoring/prep.md) step.

1. At the top of the Configuration page, click on 'Dashboards' and select `Import` beside `Prometheus 2.0 Stats` - this will bring in a pre-built dashboard for monitoring the Prometheus service itself


### Import a pre-built Kafka dashboard

1. In the left pane click on the Dashboard icon (4 squares), then `Manage`

1. Click Import