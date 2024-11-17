《資料來源》
https://www.intel.com/content/www/us/en/developer/articles/tool/intel-decimal-floating-point-math-library.html

《專案簡述》
　－－
　此為 Cmake 之下導入 Makefile 的範例。
　此中 Makefile 媒介 Cmake 進行編譯作業。此中 Makefile 編譯結果被包裝為 CmakeLibrary。
　－－
　此中使用「Intel® Decimal Floating-Point Math Library」作為示範素材。編譯資源為「IntelRDFPMathLib20U2.tar.gz」，編譯結果為「libbid.a」。
　Cmake 之下，使用 add_subdirectory() 導入當前專案，即可獲得名為 "ExternalProject::bid" 的 CmakeLibrary。

