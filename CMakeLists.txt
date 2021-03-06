# ----------------------------------------------------------------------------
# ����������� ������ CMake, ��������� ���������� ���� ����
# ----------------------------------------------------------------------------
cmake_minimum_required(VERSION 2.8)
project(MultitargetTracker)

set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

# ---------------------------------------------------------------------------- 
# ������������, ��� FindOpenCV.cmake ���������� �� ������ CMAKE_MODULE_PATH.
# ----------------------------------------------------------------------------
  FIND_PACKAGE(OpenCV)
# ----------------------------------------------------------------------------  
# ���� ��� .cpp � .h ����� � ��������� �� � ��� ������ 
# ----------------------------------------------------------------------------
  set(folder_source  main.cpp
		     Detector/Detector.cpp
                     HungarianAlg/HungarianAlg.cpp
                     KalmanFilter/Kalman.cpp
vibe_src/BackgroundSubtract.cpp
vibe_src/VIBE.cpp
                     Tracker/Ctracker.cpp)

  set(folder_header  Detector/Detector.h
		     HungarianAlg/HungarianAlg.h
                     KalmanFilter/Kalman.h
vibe_src/BackgroundSubtract.h
vibe_src/VIBE.h
                     Tracker/Ctracker.h)

  SOURCE_GROUP("Source Files" FILES ${folder_source})
  SOURCE_GROUP("Header Files" FILES ${folder_header})
# ----------------------------------------------------------------------------  
# ������� ������
# ----------------------------------------------------------------------------
  ADD_EXECUTABLE(MultitargetTracker ${folder_source} ${folder_header})
# ----------------------------------------------------------------------------   
# ��������� include ����������
# ----------------------------------------------------------------------------
  INCLUDE_DIRECTORIES(
		      ${PROJECT_SOURCE_DIR}/Detector
		      ${PROJECT_SOURCE_DIR}/HungarianAlg
		      ${PROJECT_SOURCE_DIR}/KalmanFilter
                      ${PROJECT_SOURCE_DIR}/Tracker
		      ${PROJECT_SOURCE_DIR}/vibe_src)

  INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR})
  INCLUDE_DIRECTORIES(${OpenCV_INCLUDE_DIRS})
# ----------------------------------------------------------------------------
# � Lib-� opencv 
# ----------------------------------------------------------------------------
  TARGET_LINK_LIBRARIES(MultitargetTracker ${OpenCV_LIBS})
