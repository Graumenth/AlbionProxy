#include <windows.h>
#include <tlhelp32.h>
#include <string>

bool isProcessRunning(const std::wstring& processName) {
    PROCESSENTRY32 entry;
    entry.dwSize = sizeof(PROCESSENTRY32);
    HANDLE snapshot = CreateToolhelp32Snapshot(TH32CS_SNAPPROCESS, 0);
    if (!Process32First(snapshot, &entry)) return false;
    do {
        if (std::wstring(entry.szExeFile) == processName) {
            CloseHandle(snapshot);
            return true;
        }
    } while (Process32Next(snapshot, &entry));
    CloseHandle(snapshot);
    return false;
}

int main() {
    const char* batPath = "F:\\Downloads\\AlbionStarter.bat";
    STARTUPINFOA si = { sizeof(si) };
    PROCESS_INFORMATION pi;
    CreateProcessA(NULL, (LPSTR)batPath, NULL, NULL, FALSE, CREATE_NO_WINDOW, NULL, NULL, &si, &pi);

    while (isProcessRunning(L"AlbionLauncher.exe")) {
        Sleep(5000);
    }
    return 0;
}
