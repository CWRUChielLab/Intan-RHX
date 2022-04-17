# Run with nmake, mingw32-make, or similar
# Assumes Windows 64-bit

BUILD_DIR  	= build
BUILD_TYPE 	= release
EXEC_FILE  	= IntanRHX.exe
DEPLOY_DIR 	= $(BUILD_DIR)\$(BUILD_TYPE)-deploy
BUILD_EXEC 	= $(BUILD_DIR)\$(BUILD_TYPE)\$(EXEC_FILE)
DEPLOY_EXEC	= $(DEPLOY_DIR)\$(EXEC_FILE)

COPY_FILE = copy /y
MKDIR     = mkdir
DEL_DIR   = rmdir /s

first: $(DEPLOY_EXEC)

$(BUILD_EXEC): FORCE
	if not exist $(BUILD_DIR) $(MKDIR) $(BUILD_DIR)
	cd $(BUILD_DIR)
	qmake ..\IntanRHX.pro
	$(MAKE) $(BUILD_TYPE)
	cd ..

$(DEPLOY_DIR)\kernel.cl:
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	$(COPY_FILE) kernel.cl $(DEPLOY_DIR)

$(DEPLOY_DIR)\okFrontPanel.dll:
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	$(COPY_FILE) libraries\Windows\okFrontPanel.dll $(DEPLOY_DIR)

$(DEPLOY_DIR)\ConfigRHDController.bit:
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	$(COPY_FILE) FPGA-bitfiles\ConfigRHDController.bit $(DEPLOY_DIR)

$(DEPLOY_DIR)\ConfigRHDInterfaceBoard.bit:
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	$(COPY_FILE) FPGA-bitfiles\ConfigRHDInterfaceBoard.bit $(DEPLOY_DIR)

$(DEPLOY_DIR)\ConfigRHSController.bit:
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	$(COPY_FILE) FPGA-bitfiles\ConfigRHSController.bit $(DEPLOY_DIR)

$(DEPLOY_DIR)\ConfigXEM6010Tester.bit:
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	$(COPY_FILE) FPGA-bitfiles\ConfigXEM6010Tester.bit $(DEPLOY_DIR)

$(DEPLOY_DIR)\USBEvaluationBoard.bit:
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	$(COPY_FILE) FPGA-bitfiles\USBEvaluationBoard.bit $(DEPLOY_DIR)

$(DEPLOY_DIR)\COPYING:
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	$(COPY_FILE) COPYING $(DEPLOY_DIR)

$(DEPLOY_DIR)\README.txt: FORCE
	if not exist $(DEPLOY_DIR) $(MKDIR) $(DEPLOY_DIR)
	echo Source code:> $@
	echo https://github.com/CWRUChielLab/Intan-RHX >> $@
	echo.>> $@
	echo Version:>> $@
	git describe --tags >> $@
	echo.>> $@
	echo Branch:>> $@
	git branch --show-current >> $@
	echo.>> $@
	echo Revision:>> $@
	git rev-parse HEAD >> $@
	echo.>> $@
	echo Build:>> $@
	echo Windows 64-bit ($(BUILD_TYPE)) >> $@

$(DEPLOY_EXEC): $(BUILD_EXEC) \
				$(DEPLOY_DIR)\kernel.cl \
				$(DEPLOY_DIR)\okFrontPanel.dll \
				$(DEPLOY_DIR)\ConfigRHDController.bit \
				$(DEPLOY_DIR)\ConfigRHDInterfaceBoard.bit \
				$(DEPLOY_DIR)\ConfigRHSController.bit \
				$(DEPLOY_DIR)\ConfigXEM6010Tester.bit \
				$(DEPLOY_DIR)\USBEvaluationBoard.bit \
				$(DEPLOY_DIR)\COPYING \
				$(DEPLOY_DIR)\README.txt
	windeployqt --dir $(DEPLOY_DIR) $(BUILD_EXEC)
	$(COPY_FILE) $(BUILD_EXEC) $(DEPLOY_DIR)

clean: FORCE
	if exist $(BUILD_DIR) $(DEL_DIR) $(BUILD_DIR)

FORCE:
