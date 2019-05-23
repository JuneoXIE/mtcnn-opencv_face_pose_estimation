# mtcnn-opencv_face_pose_estimation
Use mtcnn to obtain 5 face key points and estimate face pose by cv2.solvePnP

## Steps:
- mtcnn网络进行人脸检测输出bbox及脸部5个关键点(test.py) 
    - Left eye
    - Right eye
    - Nose tip
    - Left mouth corner
    - Right mouth corner  
 
- 利用opencv solvePnP 估计脸部姿态, 得到rotation vector和 transition vector(pose_estimate.py)  

3D标准脸部5个关键点模板： 
``````
model_3d_points = np.array(([-165.0, 170.0, -115.0],  # Left eye 
								[165.0, 170.0, -115.0],   # Right eye
								[0.0, 0.0, 0.0],          # Nose tip
								[-150.0, -150.0, -125.0], # Left Mouth corner
								[150.0, -150.0, -125.0]), dtype=np.double) # Right Mouth corner)
``````  
相机姿态及相关参数：
``````
focal_length = img_size[1]
	center =  [img_size[1]/2, img_size[0]/2]
	camera_matrix = np.array(([focal_length, 0, center[0]],
							[0, focal_length, center[1]],
							[0, 0, 1]),dtype=np.double)


	dist_coeffs = np.array([0,0,0,0], dtype=np.double)
``````
- 利用公式将rotation vector转化为欧拉角yaw， pitch 和 roll
