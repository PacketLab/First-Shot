# [PacketLab COVID-19 Project `data.jsonl` Format Specification](http://pktlab.caida.org:20557/data.jsonl)
###### tags: `pktlab`
> By Tzu-Bin Yan on 2020/05/16

### Per line general format
Same as specified in the GitHub issue [page](https://github.com/CAIDA/packletlab-viz/issues/1), the format for each line of the JSONL file is specified as follows:
```
{"monitor": ID, "ip": publicIP, "exp": expName, "success": result, "start": stime, "end": etime, "data": expData}
```
- `ID`: Type string, ID of the monitor
- `publicIP`: Type string, public IP of the monitor as seen from the controller side
- `expName`: Type string, name of the ran experiment
- `result`: Type number (int), either 0 or 1, indicating failure or success of the experiment respectively
- `stime`: Type number (real) (i.e. float), epoch time when starting experiment 
- `etime`: Type number (real) (i.e. float), epoch time when finishing experiment
- `expData`: JSON Object, additional information for the ran experiment

### `data` field
The `expData` field present in the per line JSON object stores an object containing different fields for different experiments, which are specified as follows:

#### `DNS_quad_1`, `DNS_quad_8`, `DNS_quad_9`, `DNS_quad_101`
For this set of experiments, the `expData` JSON object follows the following format:
```
{"response": rspString, "end_stime": endpointSendTime, "end_rtime": endpointRecvTime, "ctrl_stime": controllerSendTime, "ctrl_rtime": controllerRecvTime}
```
- `rspString`: Type string, base64 encoded DNS query response
- `endpointSendTime`: Type number (int), endpoint time (epoch time in nano second precision) when DNS query sent
- `endpointRecvTime`: Type number (int), endpoint time (epoch time in nano second precision) when DNS response received
- `controllerSendTime`: Type number (int), controller time (epoch time in nano second precision) when sending one of the PacketLab messages in the experiment (for endpoint controller latency calculation)
- `controllerRecvTime`: Type number (int), controller time (epoch time in nano second precision) when receiving the corresponding response for the PacketLab message related to `controllerSendTime` (for endpoint controller latency calculation)

#### (Other experiments to be added)