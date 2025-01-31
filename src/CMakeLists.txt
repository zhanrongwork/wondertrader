CMAKE_MINIMUM_REQUIRED(VERSION 3.0.0)

PROJECT(WonderTrader)

#3. 环境判断
IF (WIN32)
	MESSAGE(STATUS "Operation System is windows")
ELSEIF (UNIX)
	MESSAGE(STATUS "Operation System is UNIX-like OS's")
ENDIF ()

MESSAGE(STATUS "Generator is ${CMAKE_GENERATOR}")

IF (MSVC)
	ADD_DEFINITIONS (-D_CRT_SECURE_NO_WARNINGS)
	IF(CMAKE_CL_64)
		SET(INCS $ENV{MyDepends141}/include)
		SET(LNKS $ENV{MyDepends141}/lib/x64)

		MESSAGE(STATUS "MyDepends is at $ENV{MyDepends141}")
		MESSAGE(STATUS "Platform is x64")
		SET(PLATFORM x64)
	ELSE()
		SET(INCS $ENV{MyDepends141}/include)
		SET(LNKS $ENV{MyDepends141}/lib/x86)

		MESSAGE(STATUS "MyDepends is at $ENV{MyDepends141}")
		MESSAGE(STATUS "Platform is x86")
		SET(PLATFORM x86)
	ENDIF()
	SET(PREFIX )
	SET(SUFFIX .dll)
ELSE (GNUCC)
	IF(WIN32)
		SET (MyDeps $ENV{MyDependsGcc})
		SET(SUFFIX .dll)

		MESSAGE(STATUS "MyDepends is at $ENV{MyDependsGcc}")
	ELSE(UNIX)
		SET (MyDeps "/home/mydeps")
		SET(SUFFIX .so)

		MESSAGE(STATUS "MyDepends is at /home/mydeps")
	ENDIF()

	SET(INCS ${MyDeps}/include)
	SET(LNKS ${MyDeps}/lib)

	MESSAGE(STATUS "Platform is x64")
	SET(PLATFORM x64)
	SET(PREFIX lib)
ENDIF()

# BaseLibs
ADD_SUBDIRECTORY(WTSUtils)
ADD_SUBDIRECTORY(WTSTools)

# Tools
ADD_SUBDIRECTORY(CTPLoader)
ADD_SUBDIRECTORY(CTPOptLoader)
ADD_SUBDIRECTORY(LoaderRunner)
ADD_SUBDIRECTORY(MiniLoader)
ADD_SUBDIRECTORY(TraderDumper)
ADD_SUBDIRECTORY(WtMsgQue)

# Parsers
# ADD_SUBDIRECTORY(ParserAresClt)
ADD_SUBDIRECTORY(ParserCTP)
ADD_SUBDIRECTORY(ParserCTPMini)
ADD_SUBDIRECTORY(ParserCTPOpt)
ADD_SUBDIRECTORY(ParserFemas)
# ADD_SUBDIRECTORY(ParserHuaX)
# ADD_SUBDIRECTORY(ParserMA)
# ADD_SUBDIRECTORY(ParserOES)
ADD_SUBDIRECTORY(ParserUDP)
ADD_SUBDIRECTORY(ParserXeleSkt)
ADD_SUBDIRECTORY(ParserXTP)
ADD_SUBDIRECTORY(ParserYD)

# Traders
# ADD_SUBDIRECTORY(TraderAresClt)
# ADD_SUBDIRECTORY(TraderATP)
ADD_SUBDIRECTORY(TraderCTP)
ADD_SUBDIRECTORY(TraderCTPMini)
ADD_SUBDIRECTORY(TraderCTPOpt)
ADD_SUBDIRECTORY(TraderFemas)
# ADD_SUBDIRECTORY(TraderHuaX)
# ADD_SUBDIRECTORY(TraderMAOpt)
ADD_SUBDIRECTORY(TraderMocker)
# ADD_SUBDIRECTORY(TraderOES)
ADD_SUBDIRECTORY(TraderXTP)
ADD_SUBDIRECTORY(TraderXTPXAlgo)
ADD_SUBDIRECTORY(TraderYD)

# DataKit
ADD_SUBDIRECTORY(WtDtCore)
ADD_SUBDIRECTORY(WtDataStorage)
ADD_SUBDIRECTORY(WtDataStorageAD)
ADD_SUBDIRECTORY(WtDtHelper)
ADD_SUBDIRECTORY(WtDtPorter)
ADD_SUBDIRECTORY(WtDtServo)
ADD_SUBDIRECTORY(QuoteFactory)

# Plugins
ADD_SUBDIRECTORY(WtCtaStraFact)
ADD_SUBDIRECTORY(WtExeFact)
ADD_SUBDIRECTORY(WtHftStraFact)
ADD_SUBDIRECTORY(WtRiskMonFact)
ADD_SUBDIRECTORY(WtSelStraFact)

# Product
ADD_SUBDIRECTORY(WtCore)
ADD_SUBDIRECTORY(WtExecMon)
ADD_SUBDIRECTORY(WtPorter)
ADD_SUBDIRECTORY(WtRunner)

# Backtest
ADD_SUBDIRECTORY(WtBtCore)
ADD_SUBDIRECTORY(WtBtPorter)
ADD_SUBDIRECTORY(WtBtRunner)

# UltraFT
ADD_SUBDIRECTORY(WtUftCore)
ADD_SUBDIRECTORY(WtUftRunner)
ADD_SUBDIRECTORY(WtUftStraFact)

# Tests
ADD_SUBDIRECTORY(TestBtPorter)
ADD_SUBDIRECTORY(TestDtPorter)
ADD_SUBDIRECTORY(TestExecPorter)
ADD_SUBDIRECTORY(TestParser)
ADD_SUBDIRECTORY(TestPorter)
ADD_SUBDIRECTORY(TestTrader)
ADD_SUBDIRECTORY(TestUnits)
ADD_SUBDIRECTORY(WtLatencyHFT)
ADD_SUBDIRECTORY(WtLatencyUFT)

# Only used on win
IF(MSVC)
ADD_SUBDIRECTORY(TestTrader)
ENDIF()

