CGFloat imageY ;
imageY = button.imageView.frame.size.height/2.0;
CGFloat titleY ;
titleY = button.imageView.frame.size.height+5;
CGFloat imageX ;
imageX = button.titleLabel.frame.size.width/2.0+button.imageView.frame.size.width/2;
//先image 后 文字 相对坐标
button.imageEdgeInsets = UIEdgeInsetsMake(-imageY, imageX, 0, 0);
button.titleEdgeInsets = UIEdgeInsetsMake(titleY, -button.imageEdgeInsets.left, 0, 0);
