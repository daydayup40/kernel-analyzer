set (KASource
  Flags.h
  Common.h
  Global.h
  KAMain.cc
  Annotation.h
  Annotation.cc
  StructAnalyzer.h
  StructAnalyzer.cc
  CallGraph.h
  CallGraph.cc
  SafeStack.h
  SafeStack.cc
  CRange.h
  Range.h
  Range.cc
  LinuxSS.h
  LinuxSS.cc
)

# Build libraries.
add_library (KAObj OBJECT ${KASource})
# add_library (KAShared SHARED $<TARGET_OBJECTS:KAObj>)
add_library (KAStatic STATIC $<TARGET_OBJECTS:KAObj>)

# Build executable, KAMain.
set (EXECUTABLE_OUTPUT_PATH ${KA_BINARY_DIR})
link_directories (${KA_BINARY_DIR}/lib)
add_executable(KAMain ${KASource})
target_link_libraries(KAMain 
  LLVMAsmParser
  LLVMSupport
  LLVMCore
  LLVMAnalysis
  LLVMIRReader
  KAStatic
  )
