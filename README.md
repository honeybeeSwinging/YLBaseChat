# YLBaseChat
聊天界面封装，快速开发。

// 下载后需要 pod install 一下                                  
RealmSwift   数据库                            
SnapKit      约束                                  
YYText       图文             
UITableView+FDTemplateLayoutCell  自动适配高度                               
TZImagePickerController 选择相册                              

YLReplyView 输入框的封装
![image](https://github.com/zhuyunlongYL/YLBaseChat/blob/master/RImage/1.png)


    //------子类可以重写/外部调用------
    
    // 添加表情面板
    func efAddFacePanelView() -> UIView {
        
        let faceView:YLFaceView = Bundle.main.loadNibNamed("YLFaceView", owner: self, options: nil)?.first as! YLFaceView
        
        faceView.delegate = self
        
        return faceView
    }
    
    // 添加更多面板
    func efAddMorePanelView() -> UIView {
        let panelView = UIView()
        panelView.backgroundColor = UIColor.white
        
        let imageView = UIImageView()
        imageView.image = UIImage(named: "btn_import_photo")
        panelView.addSubview(imageView)
        
        imageView.snp.makeConstraints { (make) in
            make.top.equalTo(20)
            make.left.equalTo(40)
            make.width.height.equalTo(55)
        }
        
        imageView.isUserInteractionEnabled = true
        imageView.addGestureRecognizer(UITapGestureRecognizer.init(target: self, action: #selector(YLReplyView.efHandlePhotos)))
        
        return panelView
    }
    
    // 已经恢复普通状态
    func efDidRecoverReplyViewStateForNormal() {}
    
    // 已经恢复编辑状态
    func efDidRecoverReplyViewStateForEdit() {}
    
    // 收起输入框
    func efPackUpInputView() {
        updateReplyViewState(YLReplyViewState.normal)
    }
    
    // 录音处理
    func efStartRecording() {
        recordingView.recordingState = RecordingState.volumn
        recordingView.volume = 0.0
    }
    func efCancelRecording() {
        recordingView.isHidden = true
    }
    func efSendRecording() {
        recordingView.recordingState = RecordingState.timeTooShort
    }
    func efSlideUpToCancelTheRecording() {
        recordingView.recordingState = RecordingState.volumn
    }
    func efLoosenCancelRecording() {
        recordingView.recordingState = RecordingState.cancel
    }
    
    // 发送消息
    func efSendMessageText(_ text:String) {}
    func efSendMessageImage(_ images:[UIImage]?) {}
