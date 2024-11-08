# Status count

count(kql='labels.appd_name : "<application_name>" AND destination.address: "<host_name>"  and (labels.request.base_path : "/health" or labels.request.base_path : "/")')

# Status code 200

count(kql='http.response.status_code=200 and labels.appd_name : "<application_name>" AND destination.address: "<host_name>"  and (labels.request.base_path : "/health" or labels.request.base_path : "/")')

# Status code 40*

count(kql='(http.response.status_code=400 or http.response.status_code=401 or http.response.status_code=402 or http.response.status_code=403 or http.response.status_code=404) AND labels.appd_name : "<application_name>" AND destination.address: "<host_name>"  and (labels.request.base_path : "/health" or labels.request.base_path : "/")')

# Status code 50*

count(kql='(http.response.status_code=500 or http.response.status_code=501 or http.response.status_code=502 or http.response.status_code=503 or http.response.status_code=504) AND labels.appd_name : "<application_name>" AND destination.address: "<host_name>"  and (labels.request.base_path : "/health" or labels.request.base_path : "/")')