---
layout: post
Title: "[Blockchain] Hyperledger peer "
Author: bosco lyu
Date: February 1, 2018
Meta: "IT, GO"
---

* peer 
    * chain code
        * go language만 지원하면 Java는 지원하지 않음.
```
chaincodeLang = strings.ToUpper(chaincodeLang)
if pb.ChaincodeSpec_Type_value[chaincodeLang] == int32(pb.ChaincodeSpec_JAVA) {
    return nil, fmt.Errorf("Java chaincode is work-in-progress and disabled")
}
```

        * install
            * orderer 필요없음. endorser 필요함.
        * instantiate : 
            * orderer 필요함. endorser 필요함
            * env = instantiate()
                * getChaincodeSpec()
                    * checkChaincodeCmdParams()
                        * chain code name check
                        * version check (install, instantiate, upgrade, package)
                        * 
                * getChaincodeDeploymentSpec()
                * cf.Signer.Serialize()
                * utils.CreateDeployProposalFromCDS()
                * utils.GetSignedProposal()
                * cf.EndorserClient.ProcessProposal()
                * utils.CreateSignedTx()
            * cf.Boradcastclient.Send(env)
        * invoke
        * package
        * query
        * upgrade
        * signpackage
    * channel
        * create
        * join
        * fetch
        * list
        * update
    * node
        * start : 
        * status
    * logging
