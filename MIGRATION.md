# 基础控件库 适配清单

目标：把 `views/` 里的页面改成只依赖 `PCL.Modular.Abstractions` 的契约，不再直接摸全局状态。

## 全局符号依赖（按文件）

| 文件 | 行数 | 仍在直接引用的全局符号 |
| --- | --- | --- |
| `MyButton.xaml.vb` | 176 | — |
| `MyCard.vb` | 359 | `FrmMain`×1、`RunInUi`×1、`ModAnimation`×1 |
| `MyCheckBox.xaml.vb` | 230 | — |
| `MyComboBox.vb` | 173 | `FrmMain`×1 |
| `MyComboBoxItem.vb` | 67 | — |
| `MyDropShadow.vb` | 324 | — |
| `MyExtraButton.xaml.vb` | 217 | `RunInUi`×2 |
| `MyExtraTextButton.xaml.vb` | 163 | `RunInUi`×1 |
| `MyHint.xaml.vb` | 148 | `Settings`×2、`ModAnimation`×1 |
| `MyIconButton.xaml.vb` | 187 | `ModAnimation`×1 |
| `MyIconTextButton.xaml.vb` | 173 | — |
| `MyImage.vb` | 156 | `RunInUi`×1 |
| `MyListItem.xaml.vb` | 658 | — |
| `MyLoading.xaml.vb` | 276 | `RunInUi`×1 |
| `MyMenuItem.vb` | 62 | `Settings`×1 |
| `MyPageLeft.vb` | 108 | — |
| `MyPageRight.vb` | 513 | `RunInUi`×2 |
| `MyRadioBox.xaml.vb` | 252 | — |
| `MyRadioButton.xaml.vb` | 262 | — |
| `MyResizer.vb` | 315 | — |
| `MyScrollBar.vb` | 51 | — |
| `MyScrollViewer.vb` | 46 | `FrmMain`×3 |
| `MySearchBox.xaml.vb` | 45 | — |
| `MySlider.xaml.vb` | 210 | `FrmMain`×1 |
| `MySliderDot.xaml.vb` | 169 | `FrmMain`×1、`Hint`×1 |
| `MyTextBox.vb` | 322 | `RunInUi`×1 |
| `MyTextButton.vb` | 87 | — |
| `MyVirtualizingElement.vb` | 70 | — |

## 适配步骤

1. **换数据来源**：把 `ModMain` / `States` 的读取改成 `IModuleContext.Services` 里对应的服务调用。
2. **换宿主窗口引用**：`FrmMain.PanXXX` 这类直接操作宿主控件的代码，改成通过 `IHostShell` 暴露的插槽。
3. **换提示**：`Hint` / `MyMsgBox` 改成 `INotificationService`。
4. **换主题**：`ThemeUnlock` 等主题开关改成 `IThemeService`。
5. 每换完一个文件，就在下表中把该行删掉；表空了才算这个模块真正独立。

> 说明：这一步是**迁移进度的账本**，不是待办愿望单。没做完的行必须留着。
