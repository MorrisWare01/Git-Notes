##### Quaternion operator *(Quaternion lhs, Quaternion rhs)
将四元数lhs和四元数rhs结合得到新的四元数
获取lhs 的旋转状态并应用rhs的旋转。
通过lhs * rhs产生的旋转是相同于按顺序逐一应用旋转：lhs 旋转然后rhs。

##### Vector3 operator *(Quaternion rotation, Vector3 point)
使用point和rotation一起旋转点。
根据rotation旋转point到一个新的方向

##### Quaternion.Euler(vector)
返回一个旋转角度，绕z轴旋转z度，绕x轴旋转x度，绕y轴旋转y度（像这样的顺序）

##### Quaternion FromToRotation(Vector3 fromDirection, Vector3 toDirection)
从fromDirection方向转到toDirection方向
一般用于变换物体其中一轴到指定方向

##### Quaternion.Slerp（Quaternion a, Quaternion b, float t）
从一个角度转到另一个角度，t表示旋转进度，0~1，0还没开始转，1已经转到目标角度

