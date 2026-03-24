# Env Variables:
HubSpot Personal Access Key = $HUBSPOT_TOKEN;
HubSpot User ID = $HUBSPOT_USER_ID;
Sequence ID = 582602486;


# Notes
We're trying to make an automation for HubSpot using data fetched over API.

We need a config file, and the config file will contain an array of Sequence IDs. The app itself, probably written in Python and hosted on a DO Droplet, will iterate over each Sequence and fetch the Email IDs for each Sequence, then for each Email it will look at the events for each receiving Contact and get the Open Count for each contact. If the Open Count is greater than two, then we'll send data to a webhook and the app's responsibility will be complete. Before we can do all that however, we need to do some sanity/smoke tests of the API and account capabilities.

So that's the first thing we need to do, lay the ground work for proof-of-concept at each step. We need to establish an API connection with Hubspot and fetch Sequence IDs. I have already exported my HubSpot Personal Access Key as HUBSPOT_TOKEN and user ID as HUBSPOT_USER_ID to my env.
