
 

 

 

 

 

([C++](Cpp.md)) [QwtExample11](CppQwtExample11.md)
====================================================

 

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1

[Project type](CppQtProjectType.md):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)

[C++ standard](CppStandard.md):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppQwtExample11/CppQwtExample11.pro
------------------------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------
  ` #Qwt does not go together with Qwt include(../../DesktopApplicationNoWeffcpp.pri) include(../../Libraries/Qwt.pri)  SOURCES += main.cpp`
  --------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQwtExample11/main.cpp
--------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <cmath> #include <string> #include <string> #include <sstream>  #include <QApplication> #include <QDesktopWidget>  #include <boost/math/distributions/chi_squared.hpp>  #include <qwt_plot.h> #include <qwt_plot_curve.h> #include <qwt_column_symbol.h> #include <qwt_legend.h> #include <qwt_plot_multi_barchart.h> #include <qwt_text.h>  int main(int argc, char *argv[]) {   QApplication a(argc, argv);    const double maxx{10.0};   const double dx{0.01};    QwtPlot * const plot{new QwtPlot};    //dof: degrees of freedom   for (int dof=2; dof!=8; ++dof)   {     boost::math::chi_squared_distribution<double> distribution(dof);      QwtPlotCurve * const curve{new QwtPlotCurve};     QVector<QPointF> v;     for (double x=0.0; x < maxx; x+=dx)     {       const double y{boost::math::pdf(distribution,x)};       v.push_back(QPointF(x,y));     }      const int r{dof == 7 || dof == 2 || dof == 3 ? 255 : 0};     const int g{dof == 3 || dof == 4 || dof == 5 ? 255 : 0};     const int b{dof == 5 || dof == 6 || dof == 7 ? 255 : 0};     curve->setPen(QColor(r,g,b),2.0);     curve->setSamples(v);     curve->setTitle(QwtText(std::to_string(dof).c_str()));     curve->attach(plot);   }    plot->setTitle("Probability density function of chi-squared distribution");   plot->setAxisScale(QwtPlot::xBottom,0.0,10.0,1);   plot->setAxisScale(QwtPlot::yLeft,0.0,0.5,0.1);   plot->setAxisTitle(QwtPlot::xBottom,"x");   plot->setAxisTitle(QwtPlot::yLeft,"Density");    {     QwtLegend * const legend = new QwtLegend;     legend->setFrameStyle(QFrame::Box|QFrame::Sunken);     plot->insertLegend(legend, QwtPlot::RightLegend);   }    //Put plot in screen center   {     const QRect screen = QApplication::desktop()->screenGeometry();     plot->setGeometry(0,0,screen.width() * 8 / 10,screen.height() * 8 / 10);     plot->move(screen.center() - plot->geometry().center());   }    plot->show();   plot->replot();   return a.exec(); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

