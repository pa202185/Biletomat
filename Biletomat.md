// Biletomat //
#include <windows.h>
#include <stdio.h>
#include <math.h>
#include <cstdlib>
#include <iostream>
#include <string>
#include <windowsx.h>
#include <sstream>

#define ID_PRZYCISK1 501
#define ID_PRZYCISK2 502
#define ID_PRZYCISK3 503
#define ID_PRZYCISK4 504
#define ID_PRZYCISK5 505
#define ID_1 506
#define ID_2 507
#define ID_3 508
#define ID_4 509
#define ID_5 510
#define ID_6 511
#define ID_7 512
#define ID_8 513
#define ID_9 514

#define ID_COMBO1 530

using namespace::std;
int cena;
//int wybor = ComboBox_GetCurSel(hCombo);
int ilosc;
char NapisCombo;

//DWORD dlugosc;

HWND hCombo;
LPSTR NazwaKlasy = "Klasa okna";
MSG Komunikat;
HWND g_hPrzycisk;

LRESULT CALLBACK WndProc( HWND hwnd, UINT msg, WPARAM wParam, LPARAM lParam );

int WINAPI WinMain( HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow )
{



    // WYPEŁNIANIE STRUKTURY
    WNDCLASSEX wc;

    wc.cbSize = sizeof( WNDCLASSEX );
    wc.style = 0;
    wc.lpfnWndProc = WndProc;
    wc.cbClsExtra = 0;
    wc.cbWndExtra = 0;
    wc.hInstance = hInstance;
    wc.hIcon = LoadIcon( NULL, IDI_APPLICATION );
    wc.hCursor = LoadCursor( NULL, IDC_ARROW );
    wc.hbrBackground =( HBRUSH )( COLOR_WINDOW + 9 );
    wc.lpszMenuName = NULL;
    wc.lpszClassName = NazwaKlasy;
    wc.hIconSm = LoadIcon( NULL, IDI_APPLICATION );

    // REJESTROWANIE KLASY OKNA
    if( !RegisterClassEx( & wc ) )
    {
        MessageBox( NULL, "PROBLEM", "Nie dziala okno",
        MB_ICONEXCLAMATION | MB_OK );
        return 1;
    }

    // TWORZENIE OKNA
    HWND hwnd;

    hwnd = CreateWindowEx( WS_EX_CLIENTEDGE, NazwaKlasy, "BILETOMAT", WS_OVERLAPPEDWINDOW,
    CW_USEDEFAULT, CW_USEDEFAULT, 500, 600, NULL, NULL, hInstance, NULL );

    if( hwnd == NULL )
    {
        MessageBox( NULL, "Okno nie dziala!", "", MB_ICONEXCLAMATION );
        return 1;
    }

    g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "Bilet normalny", WS_CHILD | WS_VISIBLE,
    50, 250, 150, 30, hwnd,( HMENU ) ID_PRZYCISK1, hInstance, NULL );

    g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "Bilet ulgowy", WS_CHILD | WS_VISIBLE,
    200, 250, 150, 30, hwnd,( HMENU ) ID_PRZYCISK2, hInstance, NULL );

    g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "Bilet 24h", WS_CHILD | WS_VISIBLE,
    50, 280, 150, 30, hwnd,( HMENU ) ID_PRZYCISK3, hInstance, NULL );

    g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "Bilet strefowy", WS_CHILD | WS_VISIBLE,
    200, 280, 150, 30, hwnd,( HMENU ) ID_PRZYCISK4, hInstance, NULL );

    g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "KUP", WS_CHILD | WS_VISIBLE,
    120, 400, 150, 30, hwnd,( HMENU ) ID_PRZYCISK5, hInstance, NULL );

    g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "1", WS_CHILD | WS_VISIBLE,
    50, 50, 40, 40, hwnd,( HMENU ) ID_1, hInstance, NULL );

     g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "2", WS_CHILD | WS_VISIBLE,
    90, 50, 40, 40, hwnd,( HMENU ) ID_2, hInstance, NULL );

     g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "3", WS_CHILD | WS_VISIBLE,
    130, 50, 40, 40, hwnd,( HMENU ) ID_3, hInstance, NULL );

     g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "4", WS_CHILD | WS_VISIBLE,
    50, 90, 40, 40, hwnd,( HMENU ) ID_4, hInstance, NULL );

     g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "5", WS_CHILD | WS_VISIBLE,
    90, 90, 40, 40, hwnd,( HMENU ) ID_5, hInstance, NULL );

     g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "6", WS_CHILD | WS_VISIBLE,
    130, 90, 40, 40, hwnd,( HMENU ) ID_6, hInstance, NULL );

     g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "7", WS_CHILD | WS_VISIBLE,
    50, 130, 40, 40, hwnd,( HMENU ) ID_7, hInstance, NULL );

     g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "8", WS_CHILD | WS_VISIBLE,
    90, 130, 40, 40, hwnd,( HMENU ) ID_8, hInstance, NULL );

     g_hPrzycisk = CreateWindowEx( WS_EX_CLIENTEDGE, "BUTTON", "9", WS_CHILD | WS_VISIBLE,
    130, 130, 40, 40, hwnd,( HMENU ) ID_9, hInstance, NULL );

    g_hPrzycisk = CreateWindowEx( 0, "BUTTON", "1. Wybierz ilosc:", WS_CHILD | WS_VISIBLE | BS_GROUPBOX,
35, 30, 150, 150, hwnd, NULL, hInstance, NULL );


    g_hPrzycisk = CreateWindowEx( 0, "BUTTON", "2. Wybierz rodzaj:", WS_CHILD | WS_VISIBLE | BS_GROUPBOX,
35, 220, 330, 120, hwnd, NULL, hInstance, NULL );


    g_hPrzycisk = CreateWindowEx( 0, "BUTTON", "3. Zaplac:", WS_CHILD | WS_VISIBLE | BS_GROUPBOX,
105, 370, 180, 80, hwnd, NULL, hInstance, NULL );


    //HWND hCombo = CreateWindowEx( WS_EX_CLIENTEDGE, "COMBOBOX", NULL, WS_CHILD | WS_VISIBLE | WS_BORDER | WS_HSCROLL | WS_VSCROLL |
    //CBS_DROPDOWNLIST, 50, 50, 150, 100, hwnd, NULL, hInstance, NULL );


/*
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "1" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "2" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "3" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "4" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "5" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "6" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "7" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "8" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "9" );
    SendMessage( hCombo, CB_ADDSTRING, 0,( LPARAM ) "10" );

*/

    //int wybor = ComboBox_GetCurSel( hCombo );
   // int dlugosc = ComboBox_GetTextLength( hCombo );






    ShowWindow( hwnd, nCmdShow ); // Pokaż okienko
    UpdateWindow( hwnd );

    // Pętla komunikatów
    while( GetMessage( & Komunikat, NULL, 0, 0 ) )
    {
        TranslateMessage( & Komunikat );
        DispatchMessage( & Komunikat );
    }
    return Komunikat.wParam;
}





/////////////////////////////////////////TU ZACZYNA SIE PROBLEM
// OBSŁUGA ZDARZEŃ
LRESULT CALLBACK WndProc( HWND hwnd, UINT msg, WPARAM wParam, LPARAM lParam )
{

    char tmp [16];
    int dozaplaty = ilosc*cena;

    switch( msg )
    {
    case WM_CLOSE:
       {

        DestroyWindow( hwnd );
        break;
       }
    case WM_DESTROY:
        {

        PostQuitMessage( 0 );
        break;
        }

    case WM_COMMAND:
    switch( wParam )
{

    case ID_PRZYCISK1:

        cena= 3;
        MessageBox( hwnd, "Wybrales bilet normalny, cena 3 zl", "", MB_ICONINFORMATION );

    break;

    case ID_PRZYCISK2:


        cena = 2;
        MessageBox( hwnd, "Wybrales bilet ulgowym, cena: 2 zl", "", MB_ICONINFORMATION );

    break;

    case ID_PRZYCISK3:


        cena = 8;
        MessageBox( hwnd, "Wybrales bilet 24h, cena: 8 zl", "", MB_ICONINFORMATION );

    break;

    case ID_PRZYCISK4:

        cena = 7;
        MessageBox( hwnd, "Wybrales bilet strefowy, cena: 7 zl", "", MB_ICONINFORMATION );

    break;

     case ID_1:

        ilosc = 1;


    break;

     case ID_2:

        ilosc = 2;


    break;

     case ID_3:

        ilosc = 3;


    break;

     case ID_4:

        ilosc = 4;


    break;

     case ID_5:

        ilosc = 5;

     break;

     case ID_6:

       ilosc = 6;


    break;

     case ID_7:

        ilosc = 7;


    break;

     case ID_8:

        ilosc = 8;


    break;

    case ID_9:

        ilosc = 9;


    break;

    case ID_PRZYCISK5:


/*
        LPSTR NapisCombo1;
        ComboBox_GetText( hCombo, NapisCombo1, 9 );


        if (NapisCombo1 == "3")

        {
            ilosc = 3;
        }

*/

        int dozaplaty = ilosc * cena;

        sprintf(  tmp , "Naleznosc: %d zl", dozaplaty );
        MessageBoxA(hwnd, tmp, "BILETOMAT", MB_OK);

    break;


}
        default:
        return DefWindowProc( hwnd, msg, wParam, lParam );

    }

{

    return 0;
}
}


