---
layout: post
Title: "[Blockchain] Hyperledger peer "
Author: bosco lyu
Date: February 1, 2018
Meta: "IT, GO"
published: false
---

# peer 
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
                ```
                    type ChaincodeSpec struct {
	                    Type        ChaincodeSpec_Type `protobuf:"varint,1,opt,name=type,enum=protos.ChaincodeSpec_Type" json:"type,omitempty"`
                        ChaincodeId *ChaincodeID       `protobuf:"bytes,2,opt,name=chaincode_id,json=chaincodeId" json:"chaincode_id,omitempty"`
	                    Input       *ChaincodeInput    `protobuf:"bytes,3,opt,name=input" json:"input,omitempty"`
	                    Timeout     int32              `protobuf:"varint,4,opt,name=timeout" json:"timeout,omitempty"`  
                    }
                ```
            * getChaincodeDeploymentSpec()
                * container.GetChaincodePackageBytes(spec) : ChaincodeSpec을 Input으로 받아서 실제 언어별로 종속성 데이터 카피함.
                * pb.ChaincodeDeploymentSpec()
                ```
                    type ChaincodeDeploymentSpec struct {
	                    ChaincodeSpec *ChaincodeSpec 
	                    // Controls when the chaincode becomes executable.
	                    EffectiveDate *google_protobuf1.Timestamp             
	                    CodePackage   []byte
	                    ExecEnv       ChaincodeDeploymentSpec_ExecutionEnvironment 
                    }
                ```
            * cf.Signer.Serialize() : 사인 진행
            * utils.CreateDeployProposalFromCDS() : 
                * signer를 byte로 변환
            * utils.GetSignedProposal() : 
                * proposal을 사인하는 함수
            * cf.EndorserClient.ProcessProposal() : 
                * 사인한 proposal을 orderer로 전달함.
            * utils.CreateSignedTx()
                * 응답 결과 분해해서 envelope를 생성함.
            * cf.Boradcastclient.Send(env)
    * invoke
    * package
    * query
    * upgrade
    * signpackage
* channel
    * create
        * sendCreateChainTransaction()
            * configTx 파일에서 설정 정보를 읽어옴. unmarshalling
            * 유효성 체크함.
            * orderer로 요청함.
        * getGenesisBlock : 
        * marshal : block 정보를 marshalling함.
        * writeFile() : genesis block을 기록함.
    * join
        * 
    * fetch
    * list
    * update
* node
    * start : 
    * status
* logging
