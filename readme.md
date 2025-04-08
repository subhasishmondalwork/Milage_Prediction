<!DOCTYPE html>

<html lang="en">
<head><meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Mileage Prediction - Linear Regression Analysis</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<style type="text/css">
    pre { line-height: 125%; }
td.linenos .normal { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
span.linenos { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
td.linenos .special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .pm { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation.Marker */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/* tiny scrollbar */

.jp-scrollbar-tiny {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
  scrollbar-width: thin;
}

/* tiny scrollbar */

.jp-scrollbar-tiny::-webkit-scrollbar,
.jp-scrollbar-tiny::-webkit-scrollbar-corner {
  background-color: transparent;
  height: 4px;
  width: 4px;
}

.jp-scrollbar-tiny::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:horizontal {
  border-left: 0 solid transparent;
  border-right: 0 solid transparent;
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:vertical {
  border-top: 0 solid transparent;
  border-bottom: 0 solid transparent;
}

/*
 * Lumino
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
}

.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.lm-AccordionPanel[data-orientation='horizontal'] > .lm-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-CommandPalette-search {
  flex: 0 0 auto;
}

.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}

.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}

.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}

.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-close-icon {
  border: 1px solid transparent;
  background-color: transparent;
  position: absolute;
  z-index: 1;
  right: 3%;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 7px 0;
  display: none;
  vertical-align: middle;
  outline: 0;
  cursor: pointer;
}
.lm-close-icon:after {
  content: 'X';
  display: block;
  width: 15px;
  height: 15px;
  text-align: center;
  color: #000;
  font-weight: normal;
  font-size: 12px;
  cursor: pointer;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-DockPanel {
  z-index: 0;
}

.lm-DockPanel-widget {
  z-index: 0;
}

.lm-DockPanel-tabBar {
  z-index: 1;
}

.lm-DockPanel-handle {
  z-index: 2;
}

.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}

.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}

.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}

.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}

.lm-Menu-item {
  display: table-row;
}

.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}

.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}

.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}

.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}

.lm-MenuBar-item {
  box-sizing: border-box;
}

.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}

.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}

.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}

.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}

.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-SplitPanel-child {
  z-index: 0;
}

.lm-SplitPanel-handle {
  z-index: 1;
}

.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
  align-items: flex-end;
}

.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
  align-items: flex-end;
}

.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}

.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}

.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}

.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
  touch-action: none; /* Disable native Drag/Drop */
}

.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}

.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

.lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
}

.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar-addButton.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}

.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}

.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

.lm-TabBar-tabLabel .lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
  background: inherit;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabPanel-tabBar {
  z-index: 1;
}

.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.jp-Collapse-header {
  padding: 1px 12px;
  background-color: var(--jp-layout-color1);
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  align-items: center;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  text-transform: uppercase;
  user-select: none;
}

.jp-Collapser-icon {
  height: 16px;
}

.jp-Collapse-header-collapsed .jp-Collapser-icon {
  transform: rotate(-90deg);
  margin: auto 0;
}

.jp-Collapser-title {
  line-height: 25px;
}

.jp-Collapse-contents {
  padding: 0 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add-above: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5MikiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik00Ljc1IDQuOTMwNjZINi42MjVWNi44MDU2NkM2LjYyNSA3LjAxMTkxIDYuNzkzNzUgNy4xODA2NiA3IDcuMTgwNjZDNy4yMDYyNSA3LjE4MDY2IDcuMzc1IDcuMDExOTEgNy4zNzUgNi44MDU2NlY0LjkzMDY2SDkuMjVDOS40NTYyNSA0LjkzMDY2IDkuNjI1IDQuNzYxOTEgOS42MjUgNC41NTU2NkM5LjYyNSA0LjM0OTQxIDkuNDU2MjUgNC4xODA2NiA5LjI1IDQuMTgwNjZINy4zNzVWMi4zMDU2NkM3LjM3NSAyLjA5OTQxIDcuMjA2MjUgMS45MzA2NiA3IDEuOTMwNjZDNi43OTM3NSAxLjkzMDY2IDYuNjI1IDIuMDk5NDEgNi42MjUgMi4zMDU2NlY0LjE4MDY2SDQuNzVDNC41NDM3NSA0LjE4MDY2IDQuMzc1IDQuMzQ5NDEgNC4zNzUgNC41NTU2NkM0LjM3NSA0Ljc2MTkxIDQuNTQzNzUgNC45MzA2NiA0Ljc1IDQuOTMwNjZaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC43Ii8+CjwvZz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgOS41VjExLjVMMi41IDExLjVWOS41TDExLjUgOS41Wk0xMiA4QzEyLjU1MjMgOCAxMyA4LjQ0NzcyIDEzIDlWMTJDMTMgMTIuNTUyMyAxMi41NTIzIDEzIDEyIDEzTDIgMTNDMS40NDc3MiAxMyAxIDEyLjU1MjMgMSAxMlY5QzEgOC40NDc3MiAxLjQ0NzcxIDggMiA4TDEyIDhaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5MiI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KC0xIDAgMCAxIDEwIDEuNTU1NjYpIi8+CjwvY2xpcFBhdGg+CjwvZGVmcz4KPC9zdmc+Cg==);
  --jp-icon-add-below: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5OCkiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik05LjI1IDEwLjA2OTNMNy4zNzUgMTAuMDY5M0w3LjM3NSA4LjE5NDM0QzcuMzc1IDcuOTg4MDkgNy4yMDYyNSA3LjgxOTM0IDcgNy44MTkzNEM2Ljc5Mzc1IDcuODE5MzQgNi42MjUgNy45ODgwOSA2LjYyNSA4LjE5NDM0TDYuNjI1IDEwLjA2OTNMNC43NSAxMC4wNjkzQzQuNTQzNzUgMTAuMDY5MyA0LjM3NSAxMC4yMzgxIDQuMzc1IDEwLjQ0NDNDNC4zNzUgMTAuNjUwNiA0LjU0Mzc1IDEwLjgxOTMgNC43NSAxMC44MTkzTDYuNjI1IDEwLjgxOTNMNi42MjUgMTIuNjk0M0M2LjYyNSAxMi45MDA2IDYuNzkzNzUgMTMuMDY5MyA3IDEzLjA2OTNDNy4yMDYyNSAxMy4wNjkzIDcuMzc1IDEyLjkwMDYgNy4zNzUgMTIuNjk0M0w3LjM3NSAxMC44MTkzTDkuMjUgMTAuODE5M0M5LjQ1NjI1IDEwLjgxOTMgOS42MjUgMTAuNjUwNiA5LjYyNSAxMC40NDQzQzkuNjI1IDEwLjIzODEgOS40NTYyNSAxMC4wNjkzIDkuMjUgMTAuMDY5M1oiIGZpbGw9IiM2MTYxNjEiIHN0cm9rZT0iIzYxNjE2MSIgc3Ryb2tlLXdpZHRoPSIwLjciLz4KPC9nPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMi41IDUuNUwyLjUgMy41TDExLjUgMy41TDExLjUgNS41TDIuNSA1LjVaTTIgN0MxLjQ0NzcyIDcgMSA2LjU1MjI4IDEgNkwxIDNDMSAyLjQ0NzcyIDEuNDQ3NzIgMiAyIDJMMTIgMkMxMi41NTIzIDIgMTMgMi40NDc3MiAxMyAzTDEzIDZDMTMgNi41NTIyOSAxMi41NTIzIDcgMTIgN0wyIDdaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5OCI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KDEgMS43NDg0NmUtMDcgMS43NDg0NmUtMDcgLTEgNCAxMy40NDQzKSIvPgo8L2NsaXBQYXRoPgo8L2RlZnM+Cjwvc3ZnPgo=);
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bell: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE2IDE2IiB2ZXJzaW9uPSIxLjEiPgogICA8cGF0aCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzMzMzMzIgogICAgICBkPSJtOCAwLjI5Yy0xLjQgMC0yLjcgMC43My0zLjYgMS44LTEuMiAxLjUtMS40IDMuNC0xLjUgNS4yLTAuMTggMi4yLTAuNDQgNC0yLjMgNS4zbDAuMjggMS4zaDVjMC4wMjYgMC42NiAwLjMyIDEuMSAwLjcxIDEuNSAwLjg0IDAuNjEgMiAwLjYxIDIuOCAwIDAuNTItMC40IDAuNi0xIDAuNzEtMS41aDVsMC4yOC0xLjNjLTEuOS0wLjk3LTIuMi0zLjMtMi4zLTUuMy0wLjEzLTEuOC0wLjI2LTMuNy0xLjUtNS4yLTAuODUtMS0yLjItMS44LTMuNi0xLjh6bTAgMS40YzAuODggMCAxLjkgMC41NSAyLjUgMS4zIDAuODggMS4xIDEuMSAyLjcgMS4yIDQuNCAwLjEzIDEuNyAwLjIzIDMuNiAxLjMgNS4yaC0xMGMxLjEtMS42IDEuMi0zLjQgMS4zLTUuMiAwLjEzLTEuNyAwLjMtMy4zIDEuMi00LjQgMC41OS0wLjcyIDEuNi0xLjMgMi41LTEuM3ptLTAuNzQgMTJoMS41Yy0wLjAwMTUgMC4yOCAwLjAxNSAwLjc5LTAuNzQgMC43OS0wLjczIDAuMDAxNi0wLjcyLTAuNTMtMC43NC0wLjc5eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-bug-dot: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiPgogICAgICAgIDxwYXRoIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMTcuMTkgOEgyMFYxMEgxNy45MUMxNy45NiAxMC4zMyAxOCAxMC42NiAxOCAxMVYxMkgyMFYxNEgxOC41SDE4VjE0LjAyNzVDMTUuNzUgMTQuMjc2MiAxNCAxNi4xODM3IDE0IDE4LjVDMTQgMTkuMjA4IDE0LjE2MzUgMTkuODc3OSAxNC40NTQ5IDIwLjQ3MzlDMTMuNzA2MyAyMC44MTE3IDEyLjg3NTcgMjEgMTIgMjFDOS43OCAyMSA3Ljg1IDE5Ljc5IDYuODEgMThINFYxNkg2LjA5QzYuMDQgMTUuNjcgNiAxNS4zNCA2IDE1VjE0SDRWMTJINlYxMUM2IDEwLjY2IDYuMDQgMTAuMzMgNi4wOSAxMEg0VjhINi44MUM3LjI2IDcuMjIgNy44OCA2LjU1IDguNjIgNi4wNEw3IDQuNDFMOC40MSAzTDEwLjU5IDUuMTdDMTEuMDQgNS4wNiAxMS41MSA1IDEyIDVDMTIuNDkgNSAxMi45NiA1LjA2IDEzLjQyIDUuMTdMMTUuNTkgM0wxNyA0LjQxTDE1LjM3IDYuMDRDMTYuMTIgNi41NSAxNi43NCA3LjIyIDE3LjE5IDhaTTEwIDE2SDE0VjE0SDEwVjE2Wk0xMCAxMkgxNFYxMEgxMFYxMloiIGZpbGw9IiM2MTYxNjEiLz4KICAgICAgICA8cGF0aCBkPSJNMjIgMTguNUMyMiAyMC40MzMgMjAuNDMzIDIyIDE4LjUgMjJDMTYuNTY3IDIyIDE1IDIwLjQzMyAxNSAxOC41QzE1IDE2LjU2NyAxNi41NjcgMTUgMTguNSAxNUMyMC40MzMgMTUgMjIgMTYuNTY3IDIyIDE4LjVaIiBmaWxsPSIjNjE2MTYxIi8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yMCA4aC0yLjgxYy0uNDUtLjc4LTEuMDctMS40NS0xLjgyLTEuOTZMMTcgNC40MSAxNS41OSAzbC0yLjE3IDIuMTdDMTIuOTYgNS4wNiAxMi40OSA1IDEyIDVjLS40OSAwLS45Ni4wNi0xLjQxLjE3TDguNDEgMyA3IDQuNDFsMS42MiAxLjYzQzcuODggNi41NSA3LjI2IDcuMjIgNi44MSA4SDR2MmgyLjA5Yy0uMDUuMzMtLjA5LjY2LS4wOSAxdjFINHYyaDJ2MWMwIC4zNC4wNC42Ny4wOSAxSDR2MmgyLjgxYzEuMDQgMS43OSAyLjk3IDMgNS4xOSAzczQuMTUtMS4yMSA1LjE5LTNIMjB2LTJoLTIuMDljLjA1LS4zMy4wOS0uNjYuMDktMXYtMWgydi0yaC0ydi0xYzAtLjM0LS4wNC0uNjctLjA5LTFIMjBWOHptLTYgOGgtNHYtMmg0djJ6bTAtNGgtNHYtMmg0djJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik05IDE2LjE3TDQuODMgMTJsLTEuNDIgMS40MUw5IDE5IDIxIDdsLTEuNDEtMS40MXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBzaGFwZS1yZW5kZXJpbmc9Imdlb21ldHJpY1ByZWNpc2lvbiI+CiAgICA8cGF0aCBkPSJNNi41OSwzLjQxTDIsOEw2LjU5LDEyLjZMOCwxMS4xOEw0LjgyLDhMOCw0LjgyTDYuNTksMy40MU0xMi40MSwzLjQxTDExLDQuODJMMTQuMTgsOEwxMSwxMS4xOEwxMi40MSwxMi42TDE3LDhMMTIuNDEsMy40MU0yMS41OSwxMS41OUwxMy41LDE5LjY4TDkuODMsMTZMOC40MiwxNy40MUwxMy41LDIyLjVMMjMsMTNMMjEuNTksMTEuNTlaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTExLjQgMTguNkw2LjggMTRMMTEuNCA5LjRMMTAgOEw0IDE0TDEwIDIwTDExLjQgMTguNlpNMTYuNiAxOC42TDIxLjIgMTRMMTYuNiA5LjRMMTggOEwyNCAxNEwxOCAyMEwxNi42IDE4LjZWMTguNloiLz4KCTwvZz4KPC9zdmc+Cg==);
  --jp-icon-collapse-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNNiAxM3YyaDh2LTJ6IiAvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1jb25zb2xlLWljb24tYmFja2dyb3VuZC1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtY29uc29sZS1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIj4KICAgIDxwYXRoIGQ9Ik0xMDUgMTI3LjNoNDB2MTIuOGgtNDB6TTUxLjEgNzdMNzQgOTkuOWwtMjMuMyAyMy4zIDEwLjUgMTAuNSAyMy4zLTIzLjNMOTUgOTkuOSA4NC41IDg5LjQgNjEuNiA2Ni41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copyright: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDI0IDI0IiBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCI+CiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0xMS44OCw5LjE0YzEuMjgsMC4wNiwxLjYxLDEuMTUsMS42MywxLjY2aDEuNzljLTAuMDgtMS45OC0xLjQ5LTMuMTktMy40NS0zLjE5QzkuNjQsNy42MSw4LDksOCwxMi4xNCBjMCwxLjk0LDAuOTMsNC4yNCwzLjg0LDQuMjRjMi4yMiwwLDMuNDEtMS42NSwzLjQ0LTIuOTVoLTEuNzljLTAuMDMsMC41OS0wLjQ1LDEuMzgtMS42MywxLjQ0QzEwLjU1LDE0LjgzLDEwLDEzLjgxLDEwLDEyLjE0IEMxMCw5LjI1LDExLjI4LDkuMTYsMTEuODgsOS4xNHogTTEyLDJDNi40OCwyLDIsNi40OCwyLDEyczQuNDgsMTAsMTAsMTBzMTAtNC40OCwxMC0xMFMxNy41MiwyLDEyLDJ6IE0xMiwyMGMtNC40MSwwLTgtMy41OS04LTggczMuNTktOCw4LThzOCwzLjU5LDgsOFMxNi40MSwyMCwxMiwyMHoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-delete: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2cHgiIGhlaWdodD0iMTZweCI+CiAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIiAvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjI2MjYyIiBkPSJNNiAxOWMwIDEuMS45IDIgMiAyaDhjMS4xIDAgMi0uOSAyLTJWN0g2djEyek0xOSA0aC0zLjVsLTEtMWgtNWwtMSAxSDV2MmgxNFY0eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-duplicate: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTIuNzk5OTggMC44NzVIOC44OTU4MkM5LjIwMDYxIDAuODc1IDkuNDQ5OTggMS4xMzkxNCA5LjQ0OTk4IDEuNDYxOThDOS40NDk5OCAxLjc4NDgyIDkuMjAwNjEgMi4wNDg5NiA4Ljg5NTgyIDIuMDQ4OTZIMy4zNTQxNUMzLjA0OTM2IDIuMDQ4OTYgMi43OTk5OCAyLjMxMzEgMi43OTk5OCAyLjYzNTk0VjkuNjc5NjlDMi43OTk5OCAxMC4wMDI1IDIuNTUwNjEgMTAuMjY2NyAyLjI0NTgyIDEwLjI2NjdDMS45NDEwMyAxMC4yNjY3IDEuNjkxNjUgMTAuMDAyNSAxLjY5MTY1IDkuNjc5NjlWMi4wNDg5NkMxLjY5MTY1IDEuNDAzMjggMi4xOTA0IDAuODc1IDIuNzk5OTggMC44NzVaTTUuMzY2NjUgMTEuOVY0LjU1SDExLjA4MzNWMTEuOUg1LjM2NjY1Wk00LjE0MTY1IDQuMTQxNjdDNC4xNDE2NSAzLjY5MDYzIDQuNTA3MjggMy4zMjUgNC45NTgzMiAzLjMyNUgxMS40OTE3QzExLjk0MjcgMy4zMjUgMTIuMzA4MyAzLjY5MDYzIDEyLjMwODMgNC4xNDE2N1YxMi4zMDgzQzEyLjMwODMgMTIuNzU5NCAxMS45NDI3IDEzLjEyNSAxMS40OTE3IDEzLjEyNUg0Ljk1ODMyQzQuNTA3MjggMTMuMTI1IDQuMTQxNjUgMTIuNzU5NCA0LjE0MTY1IDEyLjMwODNWNC4xNDE2N1oiIGZpbGw9IiM2MTYxNjEiLz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNOS40MzU3NCA4LjI2NTA3SDguMzY0MzFWOS4zMzY1QzguMzY0MzEgOS40NTQzNSA4LjI2Nzg4IDkuNTUwNzggOC4xNTAwMiA5LjU1MDc4QzguMDMyMTcgOS41NTA3OCA3LjkzNTc0IDkuNDU0MzUgNy45MzU3NCA5LjMzNjVWOC4yNjUwN0g2Ljg2NDMxQzYuNzQ2NDUgOC4yNjUwNyA2LjY1MDAyIDguMTY4NjQgNi42NTAwMiA4LjA1MDc4QzYuNjUwMDIgNy45MzI5MiA2Ljc0NjQ1IDcuODM2NSA2Ljg2NDMxIDcuODM2NUg3LjkzNTc0VjYuNzY1MDdDNy45MzU3NCA2LjY0NzIxIDguMDMyMTcgNi41NTA3OCA4LjE1MDAyIDYuNTUwNzhDOC4yNjc4OCA2LjU1MDc4IDguMzY0MzEgNi42NDcyMSA4LjM2NDMxIDYuNzY1MDdWNy44MzY1SDkuNDM1NzRDOS41NTM2IDcuODM2NSA5LjY1MDAyIDcuOTMyOTIgOS42NTAwMiA4LjA1MDc4QzkuNjUwMDIgOC4xNjg2NCA5LjU1MzYgOC4yNjUwNyA5LjQzNTc0IDguMjY1MDdaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC41Ii8+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-error: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjE5IiByPSIyIi8+PHBhdGggZD0iTTEwIDNoNHYxMmgtNHoiLz48L2c+CjxwYXRoIGZpbGw9Im5vbmUiIGQ9Ik0wIDBoMjR2MjRIMHoiLz4KPC9zdmc+Cg==);
  --jp-icon-expand-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNMTEgMTBIOXYzSDZ2MmgzdjNoMnYtM2gzdi0yaC0zeiIgLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-dot: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWRvdCIgZmlsbD0iI0ZGRiI+CiAgICA8Y2lyY2xlIGN4PSIxOCIgY3k9IjE3IiByPSIzIj48L2NpcmNsZT4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-filter: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-folder-favorite: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgwVjB6IiBmaWxsPSJub25lIi8+PHBhdGggY2xhc3M9ImpwLWljb24zIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxNjE2MSIgZD0iTTIwIDZoLThsLTItMkg0Yy0xLjEgMC0yIC45LTIgMnYxMmMwIDEuMS45IDIgMiAyaDE2YzEuMSAwIDItLjkgMi0yVjhjMC0xLjEtLjktMi0yLTJ6bS0yLjA2IDExTDE1IDE1LjI4IDEyLjA2IDE3bC43OC0zLjMzLTIuNTktMi4yNCAzLjQxLS4yOUwxNSA4bDEuMzQgMy4xNCAzLjQxLjI5LTIuNTkgMi4yNC43OCAzLjMzeiIvPgo8L3N2Zz4K);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-home: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPjxwYXRoIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xMCAyMHYtNmg0djZoNXYtOGgzTDEyIDMgMiAxMmgzdjh6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-info: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUwLjk3OCA1MC45NzgiPgoJPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KCQk8cGF0aCBkPSJNNDMuNTIsNy40NThDMzguNzExLDIuNjQ4LDMyLjMwNywwLDI1LjQ4OSwwQzE4LjY3LDAsMTIuMjY2LDIuNjQ4LDcuNDU4LDcuNDU4CgkJCWMtOS45NDMsOS45NDEtOS45NDMsMjYuMTE5LDAsMzYuMDYyYzQuODA5LDQuODA5LDExLjIxMiw3LjQ1NiwxOC4wMzEsNy40NThjMCwwLDAuMDAxLDAsMC4wMDIsMAoJCQljNi44MTYsMCwxMy4yMjEtMi42NDgsMTguMDI5LTcuNDU4YzQuODA5LTQuODA5LDcuNDU3LTExLjIxMiw3LjQ1Ny0xOC4wM0M1MC45NzcsMTguNjcsNDguMzI4LDEyLjI2Niw0My41Miw3LjQ1OHoKCQkJIE00Mi4xMDYsNDIuMTA1Yy00LjQzMiw0LjQzMS0xMC4zMzIsNi44NzItMTYuNjE1LDYuODcyaC0wLjAwMmMtNi4yODUtMC4wMDEtMTIuMTg3LTIuNDQxLTE2LjYxNy02Ljg3MgoJCQljLTkuMTYyLTkuMTYzLTkuMTYyLTI0LjA3MSwwLTMzLjIzM0MxMy4zMDMsNC40NCwxOS4yMDQsMiwyNS40ODksMmM2LjI4NCwwLDEyLjE4NiwyLjQ0LDE2LjYxNyw2Ljg3MgoJCQljNC40MzEsNC40MzEsNi44NzEsMTAuMzMyLDYuODcxLDE2LjYxN0M0OC45NzcsMzEuNzcyLDQ2LjUzNiwzNy42NzUsNDIuMTA2LDQyLjEwNXoiLz4KCQk8cGF0aCBkPSJNMjMuNTc4LDMyLjIxOGMtMC4wMjMtMS43MzQsMC4xNDMtMy4wNTksMC40OTYtMy45NzJjMC4zNTMtMC45MTMsMS4xMS0xLjk5NywyLjI3Mi0zLjI1MwoJCQljMC40NjgtMC41MzYsMC45MjMtMS4wNjIsMS4zNjctMS41NzVjMC42MjYtMC43NTMsMS4xMDQtMS40NzgsMS40MzYtMi4xNzVjMC4zMzEtMC43MDcsMC40OTUtMS41NDEsMC40OTUtMi41CgkJCWMwLTEuMDk2LTAuMjYtMi4wODgtMC43NzktMi45NzljLTAuNTY1LTAuODc5LTEuNTAxLTEuMzM2LTIuODA2LTEuMzY5Yy0xLjgwMiwwLjA1Ny0yLjk4NSwwLjY2Ny0zLjU1LDEuODMyCgkJCWMtMC4zMDEsMC41MzUtMC41MDMsMS4xNDEtMC42MDcsMS44MTRjLTAuMTM5LDAuNzA3LTAuMjA3LDEuNDMyLTAuMjA3LDIuMTc0aC0yLjkzN2MtMC4wOTEtMi4yMDgsMC40MDctNC4xMTQsMS40OTMtNS43MTkKCQkJYzEuMDYyLTEuNjQsMi44NTUtMi40ODEsNS4zNzgtMi41MjdjMi4xNiwwLjAyMywzLjg3NCwwLjYwOCw1LjE0MSwxLjc1OGMxLjI3OCwxLjE2LDEuOTI5LDIuNzY0LDEuOTUsNC44MTEKCQkJYzAsMS4xNDItMC4xMzcsMi4xMTEtMC40MSwyLjkxMWMtMC4zMDksMC44NDUtMC43MzEsMS41OTMtMS4yNjgsMi4yNDNjLTAuNDkyLDAuNjUtMS4wNjgsMS4zMTgtMS43MywyLjAwMgoJCQljLTAuNjUsMC42OTctMS4zMTMsMS40NzktMS45ODcsMi4zNDZjLTAuMjM5LDAuMzc3LTAuNDI5LDAuNzc3LTAuNTY1LDEuMTk5Yy0wLjE2LDAuOTU5LTAuMjE3LDEuOTUxLTAuMTcxLDIuOTc5CgkJCUMyNi41ODksMzIuMjE4LDIzLjU3OCwzMi4yMTgsMjMuNTc4LDMyLjIxOHogTTIzLjU3OCwzOC4yMnYtMy40ODRoMy4wNzZ2My40ODRIMjMuNTc4eiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaW5zcGVjdG9yLWljb24tY29sb3IganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtanNvbi1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0Y5QTgyNSI+CiAgICA8cGF0aCBkPSJNMjAuMiAxMS44Yy0xLjYgMC0xLjcuNS0xLjcgMSAwIC40LjEuOS4xIDEuMy4xLjUuMS45LjEgMS4zIDAgMS43LTEuNCAyLjMtMy41IDIuM2gtLjl2LTEuOWguNWMxLjEgMCAxLjQgMCAxLjQtLjggMC0uMyAwLS42LS4xLTEgMC0uNC0uMS0uOC0uMS0xLjIgMC0xLjMgMC0xLjggMS4zLTItMS4zLS4yLTEuMy0uNy0xLjMtMiAwLS40LjEtLjguMS0xLjIuMS0uNC4xLS43LjEtMSAwLS44LS40LS43LTEuNC0uOGgtLjVWNC4xaC45YzIuMiAwIDMuNS43IDMuNSAyLjMgMCAuNC0uMS45LS4xIDEuMy0uMS41LS4xLjktLjEgMS4zIDAgLjUuMiAxIDEuNyAxdjEuOHpNMS44IDEwLjFjMS42IDAgMS43LS41IDEuNy0xIDAtLjQtLjEtLjktLjEtMS4zLS4xLS41LS4xLS45LS4xLTEuMyAwLTEuNiAxLjQtMi4zIDMuNS0yLjNoLjl2MS45aC0uNWMtMSAwLTEuNCAwLTEuNC44IDAgLjMgMCAuNi4xIDEgMCAuMi4xLjYuMSAxIDAgMS4zIDAgMS44LTEuMyAyQzYgMTEuMiA2IDExLjcgNiAxM2MwIC40LS4xLjgtLjEgMS4yLS4xLjMtLjEuNy0uMSAxIDAgLjguMy44IDEuNC44aC41djEuOWgtLjljLTIuMSAwLTMuNS0uNi0zLjUtMi4zIDAtLjQuMS0uOS4xLTEuMy4xLS41LjEtLjkuMS0xLjMgMC0uNS0uMi0xLTEuNy0xdi0xLjl6Ii8+CiAgICA8Y2lyY2xlIGN4PSIxMSIgY3k9IjEzLjgiIHI9IjIuMSIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSI4LjIiIHI9IjIuMSIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-julia: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDMyNSAzMDAiPgogIDxnIGNsYXNzPSJqcC1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjY2IzYzMzIj4KICAgIDxwYXRoIGQ9Ik0gMTUwLjg5ODQzOCAyMjUgQyAxNTAuODk4NDM4IDI2Ni40MjE4NzUgMTE3LjMyMDMxMiAzMDAgNzUuODk4NDM4IDMwMCBDIDM0LjQ3NjU2MiAzMDAgMC44OTg0MzggMjY2LjQyMTg3NSAwLjg5ODQzOCAyMjUgQyAwLjg5ODQzOCAxODMuNTc4MTI1IDM0LjQ3NjU2MiAxNTAgNzUuODk4NDM4IDE1MCBDIDExNy4zMjAzMTIgMTUwIDE1MC44OTg0MzggMTgzLjU3ODEyNSAxNTAuODk4NDM4IDIyNSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzM4OTgyNiI+CiAgICA8cGF0aCBkPSJNIDIzNy41IDc1IEMgMjM3LjUgMTE2LjQyMTg3NSAyMDMuOTIxODc1IDE1MCAxNjIuNSAxNTAgQyAxMjEuMDc4MTI1IDE1MCA4Ny41IDExNi40MjE4NzUgODcuNSA3NSBDIDg3LjUgMzMuNTc4MTI1IDEyMS4wNzgxMjUgMCAxNjIuNSAwIEMgMjAzLjkyMTg3NSAwIDIzNy41IDMzLjU3ODEyNSAyMzcuNSA3NSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzk1NThiMiI+CiAgICA8cGF0aCBkPSJNIDMyNC4xMDE1NjIgMjI1IEMgMzI0LjEwMTU2MiAyNjYuNDIxODc1IDI5MC41MjM0MzggMzAwIDI0OS4xMDE1NjIgMzAwIEMgMjA3LjY3OTY4OCAzMDAgMTc0LjEwMTU2MiAyNjYuNDIxODc1IDE3NC4xMDE1NjIgMjI1IEMgMTc0LjEwMTU2MiAxODMuNTc4MTI1IDIwNy42Nzk2ODggMTUwIDI0OS4xMDE1NjIgMTUwIEMgMjkwLjUyMzQzOCAxNTAgMzI0LjEwMTU2MiAxODMuNTc4MTI1IDMyNC4xMDE1NjIgMjI1Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgPGcgY2xhc3M9ImpwLWp1cHl0ZXItaWNvbi1jb2xvciIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgIDxnIGNsYXNzPSJqcC1qdXB5dGVyLWljb24tY29sb3IiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launch: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMzIgMzIiIHdpZHRoPSIzMiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yNiwyOEg2YTIuMDAyNywyLjAwMjcsMCwwLDEtMi0yVjZBMi4wMDI3LDIuMDAyNywwLDAsMSw2LDRIMTZWNkg2VjI2SDI2VjE2aDJWMjZBMi4wMDI3LDIuMDAyNywwLDAsMSwyNiwyOFoiLz4KICAgIDxwb2x5Z29uIHBvaW50cz0iMjAgMiAyMCA0IDI2LjU4NiA0IDE4IDEyLjU4NiAxOS40MTQgMTQgMjggNS40MTQgMjggMTIgMzAgMTIgMzAgMiAyMCAyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4K);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-move-down: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMTIuNDcxIDcuNTI4OTlDMTIuNzYzMiA3LjIzNjg0IDEyLjc2MzIgNi43NjMxNiAxMi40NzEgNi40NzEwMVY2LjQ3MTAxQzEyLjE3OSA2LjE3OTA1IDExLjcwNTcgNi4xNzg4NCAxMS40MTM1IDYuNDcwNTRMNy43NSAxMC4xMjc1VjEuNzVDNy43NSAxLjMzNTc5IDcuNDE0MjEgMSA3IDFWMUM2LjU4NTc5IDEgNi4yNSAxLjMzNTc5IDYuMjUgMS43NVYxMC4xMjc1TDIuNTk3MjYgNi40NjgyMkMyLjMwMzM4IDYuMTczODEgMS44MjY0MSA2LjE3MzU5IDEuNTMyMjYgNi40Njc3NFY2LjQ2Nzc0QzEuMjM4MyA2Ljc2MTcgMS4yMzgzIDcuMjM4MyAxLjUzMjI2IDcuNTMyMjZMNi4yOTI4OSAxMi4yOTI5QzYuNjgzNDIgMTIuNjgzNCA3LjMxNjU4IDEyLjY4MzQgNy43MDcxMSAxMi4yOTI5TDEyLjQ3MSA3LjUyODk5WiIgZmlsbD0iIzYxNjE2MSIvPgo8L3N2Zz4K);
  --jp-icon-move-up: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMS41Mjg5OSA2LjQ3MTAxQzEuMjM2ODQgNi43NjMxNiAxLjIzNjg0IDcuMjM2ODQgMS41Mjg5OSA3LjUyODk5VjcuNTI4OTlDMS44MjA5NSA3LjgyMDk1IDIuMjk0MjYgNy44MjExNiAyLjU4NjQ5IDcuNTI5NDZMNi4yNSAzLjg3MjVWMTIuMjVDNi4yNSAxMi42NjQyIDYuNTg1NzkgMTMgNyAxM1YxM0M3LjQxNDIxIDEzIDcuNzUgMTIuNjY0MiA3Ljc1IDEyLjI1VjMuODcyNUwxMS40MDI3IDcuNTMxNzhDMTEuNjk2NiA3LjgyNjE5IDEyLjE3MzYgNy44MjY0MSAxMi40Njc3IDcuNTMyMjZWNy41MzIyNkMxMi43NjE3IDcuMjM4MyAxMi43NjE3IDYuNzYxNyAxMi40Njc3IDYuNDY3NzRMNy43MDcxMSAxLjcwNzExQzcuMzE2NTggMS4zMTY1OCA2LjY4MzQyIDEuMzE2NTggNi4yOTI4OSAxLjcwNzExTDEuNTI4OTkgNi40NzEwMVoiIGZpbGw9IiM2MTYxNjEiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtbm90ZWJvb2staWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-numbering: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTQgMTlINlYxOS41SDVWMjAuNUg2VjIxSDRWMjJIN1YxOEg0VjE5Wk01IDEwSDZWNkg0VjdINVYxMFpNNCAxM0g1LjhMNCAxNS4xVjE2SDdWMTVINS4yTDcgMTIuOVYxMkg0VjEzWk05IDdWOUgyM1Y3SDlaTTkgMjFIMjNWMTlIOVYyMVpNOSAxNUgyM1YxM0g5VjE1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-offline-bolt: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDIuMDJjLTUuNTEgMC05Ljk4IDQuNDctOS45OCA5Ljk4czQuNDcgOS45OCA5Ljk4IDkuOTggOS45OC00LjQ3IDkuOTgtOS45OFMxNy41MSAyLjAyIDEyIDIuMDJ6TTExLjQ4IDIwdi02LjI2SDhMMTMgNHY2LjI2aDMuMzVMMTEuNDggMjB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-pdf: url(data:image/svg+xml;base64,PHN2ZwogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMiAyMiIgd2lkdGg9IjE2Ij4KICAgIDxwYXRoIHRyYW5zZm9ybT0icm90YXRlKDQ1KSIgY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0ZGMkEyQSIKICAgICAgIGQ9Im0gMjIuMzQ0MzY5LC0zLjAxNjM2NDIgaCA1LjYzODYwNCB2IDEuNTc5MjQzMyBoIC0zLjU0OTIyNyB2IDEuNTA4NjkyOTkgaCAzLjMzNzU3NiBWIDEuNjUwODE1NCBoIC0zLjMzNzU3NiB2IDMuNDM1MjYxMyBoIC0yLjA4OTM3NyB6IG0gLTcuMTM2NDQ0LDEuNTc5MjQzMyB2IDQuOTQzOTU0MyBoIDAuNzQ4OTIgcSAxLjI4MDc2MSwwIDEuOTUzNzAzLC0wLjYzNDk1MzUgMC42NzgzNjksLTAuNjM0OTUzNSAwLjY3ODM2OSwtMS44NDUxNjQxIDAsLTEuMjA0NzgzNTUgLTAuNjcyOTQyLC0xLjgzNDMxMDExIC0wLjY3Mjk0MiwtMC42Mjk1MjY1OSAtMS45NTkxMywtMC42Mjk1MjY1OSB6IG0gLTIuMDg5Mzc3LC0xLjU3OTI0MzMgaCAyLjIwMzM0MyBxIDEuODQ1MTY0LDAgMi43NDYwMzksMC4yNjU5MjA3IDAuOTA2MzAxLDAuMjYwNDkzNyAxLjU1MjEwOCwwLjg5MDAyMDMgMC41Njk4MywwLjU0ODEyMjMgMC44NDY2MDUsMS4yNjQ0ODAwNiAwLjI3Njc3NCwwLjcxNjM1NzgxIDAuMjc2Nzc0LDEuNjIyNjU4OTQgMCwwLjkxNzE1NTEgLTAuMjc2Nzc0LDEuNjM4OTM5OSAtMC4yNzY3NzUsMC43MTYzNTc4IC0wLjg0NjYwNSwxLjI2NDQ4IC0wLjY1MTIzNCwwLjYyOTUyNjYgLTEuNTYyOTYyLDAuODk1NDQ3MyAtMC45MTE3MjgsMC4yNjA0OTM3IC0yLjczNTE4NSwwLjI2MDQ5MzcgaCAtMi4yMDMzNDMgeiBtIC04LjE0NTg1NjUsMCBoIDMuNDY3ODIzIHEgMS41NDY2ODE2LDAgMi4zNzE1Nzg1LDAuNjg5MjIzIDAuODMwMzI0LDAuNjgzNzk2MSAwLjgzMDMyNCwxLjk1MzcwMzE0IDAsMS4yNzUzMzM5NyAtMC44MzAzMjQsMS45NjQ1NTcwNiBRIDkuOTg3MTk2MSwyLjI3NDkxNSA4LjQ0MDUxNDUsMi4yNzQ5MTUgSCA3LjA2MjA2ODQgViA1LjA4NjA3NjcgSCA0Ljk3MjY5MTUgWiBtIDIuMDg5Mzc2OSwxLjUxNDExOTkgdiAyLjI2MzAzOTQzIGggMS4xNTU5NDEgcSAwLjYwNzgxODgsMCAwLjkzODg2MjksLTAuMjkzMDU1NDcgMC4zMzEwNDQxLC0wLjI5ODQ4MjQxIDAuMzMxMDQ0MSwtMC44NDExNzc3MiAwLC0wLjU0MjY5NTMxIC0wLjMzMTA0NDEsLTAuODM1NzUwNzQgLTAuMzMxMDQ0MSwtMC4yOTMwNTU1IC0wLjkzODg2MjksLTAuMjkzMDU1NSB6IgovPgo8L3N2Zz4K);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iLTEwIC0xMCAxMzEuMTYxMzYxNjk0MzM1OTQgMTMyLjM4ODk5OTkzODk2NDg0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzA2OTk4IiBkPSJNIDU0LjkxODc4NSw5LjE5Mjc0MjFlLTQgQyA1MC4zMzUxMzIsMC4wMjIyMTcyNyA0NS45NTc4NDYsMC40MTMxMzY5NyA0Mi4xMDYyODUsMS4wOTQ2NjkzIDMwLjc2MDA2OSwzLjA5OTE3MzEgMjguNzAwMDM2LDcuMjk0NzcxNCAyOC43MDAwMzUsMTUuMDMyMTY5IHYgMTAuMjE4NzUgaCAyNi44MTI1IHYgMy40MDYyNSBoIC0yNi44MTI1IC0xMC4wNjI1IGMgLTcuNzkyNDU5LDAgLTE0LjYxNTc1ODgsNC42ODM3MTcgLTE2Ljc0OTk5OTgsMTMuNTkzNzUgLTIuNDYxODE5OTgsMTAuMjEyOTY2IC0yLjU3MTAxNTA4LDE2LjU4NjAyMyAwLDI3LjI1IDEuOTA1OTI4Myw3LjkzNzg1MiA2LjQ1NzU0MzIsMTMuNTkzNzQ4IDE0LjI0OTk5OTgsMTMuNTkzNzUgaCA5LjIxODc1IHYgLTEyLjI1IGMgMCwtOC44NDk5MDIgNy42NTcxNDQsLTE2LjY1NjI0OCAxNi43NSwtMTYuNjU2MjUgaCAyNi43ODEyNSBjIDcuNDU0OTUxLDAgMTMuNDA2MjUzLC02LjEzODE2NCAxMy40MDYyNSwtMTMuNjI1IHYgLTI1LjUzMTI1IGMgMCwtNy4yNjYzMzg2IC02LjEyOTk4LC0xMi43MjQ3NzcxIC0xMy40MDYyNSwtMTMuOTM3NDk5NyBDIDY0LjI4MTU0OCwwLjMyNzk0Mzk3IDU5LjUwMjQzOCwtMC4wMjAzNzkwMyA1NC45MTg3ODUsOS4xOTI3NDIxZS00IFogbSAtMTQuNSw4LjIxODc1MDEyNTc5IGMgMi43Njk1NDcsMCA1LjAzMTI1LDIuMjk4NjQ1NiA1LjAzMTI1LDUuMTI0OTk5NiAtMmUtNiwyLjgxNjMzNiAtMi4yNjE3MDMsNS4wOTM3NSAtNS4wMzEyNSw1LjA5Mzc1IC0yLjc3OTQ3NiwtMWUtNiAtNS4wMzEyNSwtMi4yNzc0MTUgLTUuMDMxMjUsLTUuMDkzNzUgLTEwZS03LC0yLjgyNjM1MyAyLjI1MTc3NCwtNS4xMjQ5OTk2IDUuMDMxMjUsLTUuMTI0OTk5NiB6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2ZmZDQzYiIgZD0ibSA4NS42Mzc1MzUsMjguNjU3MTY5IHYgMTEuOTA2MjUgYyAwLDkuMjMwNzU1IC03LjgyNTg5NSwxNi45OTk5OTkgLTE2Ljc1LDE3IGggLTI2Ljc4MTI1IGMgLTcuMzM1ODMzLDAgLTEzLjQwNjI0OSw2LjI3ODQ4MyAtMTMuNDA2MjUsMTMuNjI1IHYgMjUuNTMxMjQ3IGMgMCw3LjI2NjM0NCA2LjMxODU4OCwxMS41NDAzMjQgMTMuNDA2MjUsMTMuNjI1MDA0IDguNDg3MzMxLDIuNDk1NjEgMTYuNjI2MjM3LDIuOTQ2NjMgMjYuNzgxMjUsMCA2Ljc1MDE1NSwtMS45NTQzOSAxMy40MDYyNTMsLTUuODg3NjEgMTMuNDA2MjUsLTEzLjYyNTAwNCBWIDg2LjUwMDkxOSBoIC0yNi43ODEyNSB2IC0zLjQwNjI1IGggMjYuNzgxMjUgMTMuNDA2MjU0IGMgNy43OTI0NjEsMCAxMC42OTYyNTEsLTUuNDM1NDA4IDEzLjQwNjI0MSwtMTMuNTkzNzUgMi43OTkzMywtOC4zOTg4ODYgMi42ODAyMiwtMTYuNDc1Nzc2IDAsLTI3LjI1IC0xLjkyNTc4LC03Ljc1NzQ0MSAtNS42MDM4NywtMTMuNTkzNzUgLTEzLjQwNjI0MSwtMTMuNTkzNzUgeiBtIC0xNS4wNjI1LDY0LjY1NjI1IGMgMi43Nzk0NzgsM2UtNiA1LjAzMTI1LDIuMjc3NDE3IDUuMDMxMjUsNS4wOTM3NDcgLTJlLTYsMi44MjYzNTQgLTIuMjUxNzc1LDUuMTI1MDA0IC01LjAzMTI1LDUuMTI1MDA0IC0yLjc2OTU1LDAgLTUuMDMxMjUsLTIuMjk4NjUgLTUuMDMxMjUsLTUuMTI1MDA0IDJlLTYsLTIuODE2MzMgMi4yNjE2OTcsLTUuMDkzNzQ3IDUuMDMxMjUsLTUuMDkzNzQ3IHoiLz4KPC9zdmc+Cg==);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-redo: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIi8+PHBhdGggZD0iTTE4LjQgMTAuNkMxNi41NSA4Ljk5IDE0LjE1IDggMTEuNSA4Yy00LjY1IDAtOC41OCAzLjAzLTkuOTYgNy4yMkwzLjkgMTZjMS4wNS0zLjE5IDQuMDUtNS41IDcuNi01LjUgMS45NSAwIDMuNzMuNzIgNS4xMiAxLjg4TDEzIDE2aDlWN2wtMy42IDMuNnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-share: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTSAxOCAyIEMgMTYuMzU0OTkgMiAxNSAzLjM1NDk5MDQgMTUgNSBDIDE1IDUuMTkwOTUyOSAxNS4wMjE3OTEgNS4zNzcxMjI0IDE1LjA1NjY0MSA1LjU1ODU5MzggTCA3LjkyMTg3NSA5LjcyMDcwMzEgQyA3LjM5ODUzOTkgOS4yNzc4NTM5IDYuNzMyMDc3MSA5IDYgOSBDIDQuMzU0OTkwNCA5IDMgMTAuMzU0OTkgMyAxMiBDIDMgMTMuNjQ1MDEgNC4zNTQ5OTA0IDE1IDYgMTUgQyA2LjczMjA3NzEgMTUgNy4zOTg1Mzk5IDE0LjcyMjE0NiA3LjkyMTg3NSAxNC4yNzkyOTcgTCAxNS4wNTY2NDEgMTguNDM5NDUzIEMgMTUuMDIxNTU1IDE4LjYyMTUxNCAxNSAxOC44MDgzODYgMTUgMTkgQyAxNSAyMC42NDUwMSAxNi4zNTQ5OSAyMiAxOCAyMiBDIDE5LjY0NTAxIDIyIDIxIDIwLjY0NTAxIDIxIDE5IEMgMjEgMTcuMzU0OTkgMTkuNjQ1MDEgMTYgMTggMTYgQyAxNy4yNjc0OCAxNiAxNi42MDE1OTMgMTYuMjc5MzI4IDE2LjA3ODEyNSAxNi43MjI2NTYgTCA4Ljk0MzM1OTQgMTIuNTU4NTk0IEMgOC45NzgyMDk1IDEyLjM3NzEyMiA5IDEyLjE5MDk1MyA5IDEyIEMgOSAxMS44MDkwNDcgOC45NzgyMDk1IDExLjYyMjg3OCA4Ljk0MzM1OTQgMTEuNDQxNDA2IEwgMTYuMDc4MTI1IDcuMjc5Mjk2OSBDIDE2LjYwMTQ2IDcuNzIyMTQ2MSAxNy4yNjc5MjMgOCAxOCA4IEMgMTkuNjQ1MDEgOCAyMSA2LjY0NTAwOTYgMjEgNSBDIDIxIDMuMzU0OTkwNCAxOS42NDUwMSAyIDE4IDIgeiBNIDE4IDQgQyAxOC41NjQxMjkgNCAxOSA0LjQzNTg3MDYgMTkgNSBDIDE5IDUuNTY0MTI5NCAxOC41NjQxMjkgNiAxOCA2IEMgMTcuNDM1ODcxIDYgMTcgNS41NjQxMjk0IDE3IDUgQyAxNyA0LjQzNTg3MDYgMTcuNDM1ODcxIDQgMTggNCB6IE0gNiAxMSBDIDYuNTY0MTI5NCAxMSA3IDExLjQzNTg3MSA3IDEyIEMgNyAxMi41NjQxMjkgNi41NjQxMjk0IDEzIDYgMTMgQyA1LjQzNTg3MDYgMTMgNSAxMi41NjQxMjkgNSAxMiBDIDUgMTEuNDM1ODcxIDUuNDM1ODcwNiAxMSA2IDExIHogTSAxOCAxOCBDIDE4LjU2NDEyOSAxOCAxOSAxOC40MzU4NzEgMTkgMTkgQyAxOSAxOS41NjQxMjkgMTguNTY0MTI5IDIwIDE4IDIwIEMgMTcuNDM1ODcxIDIwIDE3IDE5LjU2NDEyOSAxNyAxOSBDIDE3IDE4LjQzNTg3MSAxNy40MzU4NzEgMTggMTggMTggeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-table-rows: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMSw4SDNWNGgxOFY4eiBNMjEsMTBIM3Y0aDE4VjEweiBNMjEsMTZIM3Y0aDE4VjE2eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-tag: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjgiIGhlaWdodD0iMjgiIHZpZXdCb3g9IjAgMCA0MyAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTI4LjgzMzIgMTIuMzM0TDMyLjk5OTggMTYuNTAwN0wzNy4xNjY1IDEyLjMzNEgyOC44MzMyWiIvPgoJCTxwYXRoIGQ9Ik0xNi4yMDk1IDIxLjYxMDRDMTUuNjg3MyAyMi4xMjk5IDE0Ljg0NDMgMjIuMTI5OSAxNC4zMjQ4IDIxLjYxMDRMNi45ODI5IDE0LjcyNDVDNi41NzI0IDE0LjMzOTQgNi4wODMxMyAxMy42MDk4IDYuMDQ3ODYgMTMuMDQ4MkM1Ljk1MzQ3IDExLjUyODggNi4wMjAwMiA4LjYxOTQ0IDYuMDY2MjEgNy4wNzY5NUM2LjA4MjgxIDYuNTE0NzcgNi41NTU0OCA2LjA0MzQ3IDcuMTE4MDQgNi4wMzA1NUM5LjA4ODYzIDUuOTg0NzMgMTMuMjYzOCA1LjkzNTc5IDEzLjY1MTggNi4zMjQyNUwyMS43MzY5IDEzLjYzOUMyMi4yNTYgMTQuMTU4NSAyMS43ODUxIDE1LjQ3MjQgMjEuMjYyIDE1Ljk5NDZMMTYuMjA5NSAyMS42MTA0Wk05Ljc3NTg1IDguMjY1QzkuMzM1NTEgNy44MjU2NiA4LjYyMzUxIDcuODI1NjYgOC4xODI4IDguMjY1QzcuNzQzNDYgOC43MDU3MSA3Ljc0MzQ2IDkuNDE3MzMgOC4xODI4IDkuODU2NjdDOC42MjM4MiAxMC4yOTY0IDkuMzM1ODIgMTAuMjk2NCA5Ljc3NTg1IDkuODU2NjdDMTAuMjE1NiA5LjQxNzMzIDEwLjIxNTYgOC43MDUzMyA5Ljc3NTg1IDguMjY1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1iYWNrZ3JvdW5kLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgd2lkdGg9IjIwIiBoZWlnaHQ9IjIwIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgyIDIpIiBmaWxsPSIjMzMzMzMzIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUtaW52ZXJzZSIgZD0iTTUuMDU2NjQgOC43NjE3MkM1LjA1NjY0IDguNTk3NjYgNS4wMzEyNSA4LjQ1MzEyIDQuOTgwNDcgOC4zMjgxMkM0LjkzMzU5IDguMTk5MjIgNC44NTU0NyA4LjA4MjAzIDQuNzQ2MDkgNy45NzY1NkM0LjY0MDYyIDcuODcxMDkgNC41IDcuNzc1MzkgNC4zMjQyMiA3LjY4OTQ1QzQuMTUyMzQgNy41OTk2MSAzLjk0MzM2IDcuNTExNzIgMy42OTcyNyA3LjQyNTc4QzMuMzAyNzMgNy4yODUxNiAyLjk0MzM2IDcuMTM2NzIgMi42MTkxNCA2Ljk4MDQ3QzIuMjk0OTIgNi44MjQyMiAyLjAxNzU4IDYuNjQyNTggMS43ODcxMSA2LjQzNTU1QzEuNTYwNTUgNi4yMjg1MiAxLjM4NDc3IDUuOTg4MjggMS4yNTk3NyA1LjcxNDg0QzEuMTM0NzcgNS40Mzc1IDEuMDcyMjcgNS4xMDkzOCAxLjA3MjI3IDQuNzMwNDdDMS4wNzIyNyA0LjM5ODQ0IDEuMTI4OTEgNC4wOTU3IDEuMjQyMTkgMy44MjIyN0MxLjM1NTQ3IDMuNTQ0OTIgMS41MTU2MiAzLjMwNDY5IDEuNzIyNjYgMy4xMDE1NkMxLjkyOTY5IDIuODk4NDQgMi4xNzk2OSAyLjczNDM3IDIuNDcyNjYgMi42MDkzOEMyLjc2NTYyIDIuNDg0MzggMy4wOTE4IDIuNDA0MyAzLjQ1MTE3IDIuMzY5MTRWMS4xMDkzOEg0LjM4ODY3VjIuMzgwODZDNC43NDAyMyAyLjQyNzczIDUuMDU2NjQgMi41MjM0NCA1LjMzNzg5IDIuNjY3OTdDNS42MTkxNCAyLjgxMjUgNS44NTc0MiAzLjAwMTk1IDYuMDUyNzMgMy4yMzYzM0M2LjI1MTk1IDMuNDY2OCA2LjQwNDMgMy43NDAyMyA2LjUwOTc3IDQuMDU2NjRDNi42MTkxNCA0LjM2OTE0IDYuNjczODMgNC43MjA3IDYuNjczODMgNS4xMTEzM0g1LjA0NDkyQzUuMDQ0OTIgNC42Mzg2NyA0LjkzNzUgNC4yODEyNSA0LjcyMjY2IDQuMDM5MDZDNC41MDc4MSAzLjc5Mjk3IDQuMjE2OCAzLjY2OTkyIDMuODQ5NjEgMy42Njk5MkMzLjY1MDM5IDMuNjY5OTIgMy40NzY1NiAzLjY5NzI3IDMuMzI4MTIgMy43NTE5NUMzLjE4MzU5IDMuODAyNzMgMy4wNjQ0NSAzLjg3Njk1IDIuOTcwNyAzLjk3NDYxQzIuODc2OTUgNC4wNjgzNiAyLjgwNjY0IDQuMTc5NjkgMi43NTk3NyA0LjMwODU5QzIuNzE2OCA0LjQzNzUgMi42OTUzMSA0LjU3ODEyIDIuNjk1MzEgNC43MzA0N0MyLjY5NTMxIDQuODgyODEgMi43MTY4IDUuMDE5NTMgMi43NTk3NyA1LjE0MDYyQzIuODA2NjQgNS4yNTc4MSAyLjg4MjgxIDUuMzY3MTkgMi45ODgyOCA1LjQ2ODc1QzMuMDk3NjYgNS41NzAzMSAzLjI0MDIzIDUuNjY3OTcgMy40MTYwMiA1Ljc2MTcyQzMuNTkxOCA1Ljg1MTU2IDMuODEwNTUgNS45NDMzNiA0LjA3MjI3IDYuMDM3MTFDNC40NjY4IDYuMTg1NTUgNC44MjQyMiA2LjMzOTg0IDUuMTQ0NTMgNi41QzUuNDY0ODQgNi42NTYyNSA1LjczODI4IDYuODM5ODQgNS45NjQ4NCA3LjA1MDc4QzYuMTk1MzEgNy4yNTc4MSA2LjM3MTA5IDcuNSA2LjQ5MjE5IDcuNzc3MzRDNi42MTcxOSA4LjA1MDc4IDYuNjc5NjkgOC4zNzUgNi42Nzk2OSA4Ljc1QzYuNjc5NjkgOS4wOTM3NSA2LjYyMzA1IDkuNDA0MyA2LjUwOTc3IDkuNjgxNjRDNi4zOTY0OCA5Ljk1NTA4IDYuMjM0MzggMTAuMTkxNCA2LjAyMzQ0IDEwLjM5MDZDNS44MTI1IDEwLjU4OTggNS41NTg1OSAxMC43NSA1LjI2MTcyIDEwLjg3MTFDNC45NjQ4NCAxMC45ODgzIDQuNjMyODEgMTEuMDY0NSA0LjI2NTYyIDExLjA5OTZWMTIuMjQ4SDMuMzMzOThWMTEuMDk5NkMzLjAwMTk1IDExLjA2ODQgMi42Nzk2OSAxMC45OTYxIDIuMzY3MTkgMTAuODgyOEMyLjA1NDY5IDEwLjc2NTYgMS43NzczNCAxMC41OTc3IDEuNTM1MTYgMTAuMzc4OUMxLjI5Njg4IDEwLjE2MDIgMS4xMDU0NyA5Ljg4NDc3IDAuOTYwOTM4IDkuNTUyNzNDMC44MTY0MDYgOS4yMTY4IDAuNzQ0MTQxIDguODE0NDUgMC43NDQxNDEgOC4zNDU3SDIuMzc4OTFDMi4zNzg5MSA4LjYyNjk1IDIuNDE5OTIgOC44NjMyOCAyLjUwMTk1IDkuMDU0NjlDMi41ODM5OCA5LjI0MjE5IDIuNjg5NDUgOS4zOTI1OCAyLjgxODM2IDkuNTA1ODZDMi45NTExNyA5LjYxNTIzIDMuMTAxNTYgOS42OTMzNiAzLjI2OTUzIDkuNzQwMjNDMy40Mzc1IDkuNzg3MTEgMy42MDkzOCA5LjgxMDU1IDMuNzg1MTYgOS44MTA1NUM0LjIwMzEyIDkuODEwNTUgNC41MTk1MyA5LjcxMjg5IDQuNzM0MzggOS41MTc1OEM0Ljk0OTIyIDkuMzIyMjcgNS4wNTY2NCA5LjA3MDMxIDUuMDU2NjQgOC43NjE3MlpNMTMuNDE4IDEyLjI3MTVIOC4wNzQyMlYxMUgxMy40MThWMTIuMjcxNVoiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMuOTUyNjQgNikiIGZpbGw9IndoaXRlIi8+Cjwvc3ZnPgo=);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtdGV4dC1lZGl0b3ItaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xNSAxNUgzdjJoMTJ2LTJ6bTAtOEgzdjJoMTJWN3pNMyAxM2gxOHYtMkgzdjJ6bTAgOGgxOHYtMkgzdjJ6TTMgM3YyaDE4VjNIM3oiLz4KPC9zdmc+Cg==);
  --jp-icon-toc: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik03LDVIMjFWN0g3VjVNNywxM1YxMUgyMVYxM0g3TTQsNC41QTEuNSwxLjUgMCAwLDEgNS41LDZBMS41LDEuNSAwIDAsMSA0LDcuNUExLjUsMS41IDAgMCwxIDIuNSw2QTEuNSwxLjUgMCAwLDEgNCw0LjVNNCwxMC41QTEuNSwxLjUgMCAwLDEgNS41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMy41QTEuNSwxLjUgMCAwLDEgMi41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMC41TTcsMTlWMTdIMjFWMTlIN000LDE2LjVBMS41LDEuNSAwIDAsMSA1LjUsMThBMS41LDEuNSAwIDAsMSA0LDE5LjVBMS41LDEuNSAwIDAsMSAyLjUsMThBMS41LDEuNSAwIDAsMSA0LDE2LjVaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tree-view: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMiAxMVYzaC03djNIOVYzSDJ2OGg3VjhoMnYxMGg0djNoN3YtOGgtN3YzaC0yVjhoMnYzeiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-user: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE2IDdhNCA0IDAgMTEtOCAwIDQgNCAwIDAxOCAwek0xMiAxNGE3IDcgMCAwMC03IDdoMTRhNyA3IDAgMDAtNy03eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-users: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAwIDM2IDI0IiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogPGcgY2xhc3M9ImpwLWljb24zIiB0cmFuc2Zvcm09Im1hdHJpeCgxLjczMjcgMCAwIDEuNzMyNyAtMy42MjgyIC4wOTk1NzcpIiBmaWxsPSIjNjE2MTYxIj4KICA8cGF0aCB0cmFuc2Zvcm09Im1hdHJpeCgxLjUsMCwwLDEuNSwwLC02KSIgZD0ibTEyLjE4NiA3LjUwOThjLTEuMDUzNSAwLTEuOTc1NyAwLjU2NjUtMi40Nzg1IDEuNDEwMiAwLjc1MDYxIDAuMzEyNzcgMS4zOTc0IDAuODI2NDggMS44NzMgMS40NzI3aDMuNDg2M2MwLTEuNTkyLTEuMjg4OS0yLjg4MjgtMi44ODA5LTIuODgyOHoiLz4KICA8cGF0aCBkPSJtMjAuNDY1IDIuMzg5NWEyLjE4ODUgMi4xODg1IDAgMCAxLTIuMTg4NCAyLjE4ODUgMi4xODg1IDIuMTg4NSAwIDAgMS0yLjE4ODUtMi4xODg1IDIuMTg4NSAyLjE4ODUgMCAwIDEgMi4xODg1LTIuMTg4NSAyLjE4ODUgMi4xODg1IDAgMCAxIDIuMTg4NCAyLjE4ODV6Ii8+CiAgPHBhdGggdHJhbnNmb3JtPSJtYXRyaXgoMS41LDAsMCwxLjUsMCwtNikiIGQ9Im0zLjU4OTggOC40MjE5Yy0xLjExMjYgMC0yLjAxMzcgMC45MDExMS0yLjAxMzcgMi4wMTM3aDIuODE0NWMwLjI2Nzk3LTAuMzczMDkgMC41OTA3LTAuNzA0MzUgMC45NTg5OC0wLjk3ODUyLTAuMzQ0MzMtMC42MTY4OC0xLjAwMzEtMS4wMzUyLTEuNzU5OC0xLjAzNTJ6Ii8+CiAgPHBhdGggZD0ibTYuOTE1NCA0LjYyM2ExLjUyOTQgMS41Mjk0IDAgMCAxLTEuNTI5NCAxLjUyOTQgMS41Mjk0IDEuNTI5NCAwIDAgMS0xLjUyOTQtMS41Mjk0IDEuNTI5NCAxLjUyOTQgMCAwIDEgMS41Mjk0LTEuNTI5NCAxLjUyOTQgMS41Mjk0IDAgMCAxIDEuNTI5NCAxLjUyOTR6Ii8+CiAgPHBhdGggZD0ibTYuMTM1IDEzLjUzNWMwLTMuMjM5MiAyLjYyNTktNS44NjUgNS44NjUtNS44NjUgMy4yMzkyIDAgNS44NjUgMi42MjU5IDUuODY1IDUuODY1eiIvPgogIDxjaXJjbGUgY3g9IjEyIiBjeT0iMy43Njg1IiByPSIyLjk2ODUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-word: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KIDxnIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzQxNDE0MSI+CiAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiA8L2c+CiA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSguNDMgLjA0MDEpIiBmaWxsPSIjZmZmIj4KICA8cGF0aCBkPSJtNC4xNCA4Ljc2cTAuMDY4Mi0xLjg5IDIuNDItMS44OSAxLjE2IDAgMS42OCAwLjQyIDAuNTY3IDAuNDEgMC41NjcgMS4xNnYzLjQ3cTAgMC40NjIgMC41MTQgMC40NjIgMC4xMDMgMCAwLjItMC4wMjMxdjAuNzE0cS0wLjM5OSAwLjEwMy0wLjY1MSAwLjEwMy0wLjQ1MiAwLTAuNjkzLTAuMjItMC4yMzEtMC4yLTAuMjg0LTAuNjYyLTAuOTU2IDAuODcyLTIgMC44NzItMC45MDMgMC0xLjQ3LTAuNDcyLTAuNTI1LTAuNDcyLTAuNTI1LTEuMjYgMC0wLjI2MiAwLjA0NTItMC40NzIgMC4wNTY3LTAuMjIgMC4xMTYtMC4zNzggMC4wNjgyLTAuMTY4IDAuMjMxLTAuMzA0IDAuMTU4LTAuMTQ3IDAuMjYyLTAuMjQyIDAuMTE2LTAuMDkxNCAwLjM2OC0wLjE2OCAwLjI2Mi0wLjA5MTQgMC4zOTktMC4xMjYgMC4xMzYtMC4wNDUyIDAuNDcyLTAuMTAzIDAuMzM2LTAuMDU3OCAwLjUwNC0wLjA3OTggMC4xNTgtMC4wMjMxIDAuNTY3LTAuMDc5OCAwLjU1Ni0wLjA2ODIgMC43NzctMC4yMjEgMC4yMi0wLjE1MiAwLjIyLTAuNDQxdi0wLjI1MnEwLTAuNDMtMC4zNTctMC42NjItMC4zMzYtMC4yMzEtMC45NzYtMC4yMzEtMC42NjIgMC0wLjk5OCAwLjI2Mi0wLjMzNiAwLjI1Mi0wLjM5OSAwLjc5OHptMS44OSAzLjY4cTAuNzg4IDAgMS4yNi0wLjQxIDAuNTA0LTAuNDIgMC41MDQtMC45MDN2LTEuMDVxLTAuMjg0IDAuMTM2LTAuODYxIDAuMjMxLTAuNTY3IDAuMDkxNC0wLjk4NyAwLjE1OC0wLjQyIDAuMDY4Mi0wLjc2NiAwLjMyNi0wLjMzNiAwLjI1Mi0wLjMzNiAwLjcwNHQwLjMwNCAwLjcwNCAwLjg2MSAwLjI1MnoiIHN0cm9rZS13aWR0aD0iMS4wNSIvPgogIDxwYXRoIGQ9Im0xMCA0LjU2aDAuOTQ1djMuMTVxMC42NTEtMC45NzYgMS44OS0wLjk3NiAxLjE2IDAgMS44OSAwLjg0IDAuNjgyIDAuODQgMC42ODIgMi4zMSAwIDEuNDctMC43MDQgMi40Mi0wLjcwNCAwLjg4Mi0xLjg5IDAuODgyLTEuMjYgMC0xLjg5LTEuMDJ2MC43NjZoLTAuODV6bTIuNjIgMy4wNHEtMC43NDYgMC0xLjE2IDAuNjQtMC40NTIgMC42My0wLjQ1MiAxLjY4IDAgMS4wNSAwLjQ1MiAxLjY4dDEuMTYgMC42M3EwLjc3NyAwIDEuMjYtMC42MyAwLjQ5NC0wLjY0IDAuNDk0LTEuNjggMC0xLjA1LTAuNDcyLTEuNjgtMC40NjItMC42NC0xLjI2LTAuNjR6IiBzdHJva2Utd2lkdGg9IjEuMDUiLz4KICA8cGF0aCBkPSJtMi43MyAxNS44IDEzLjYgMC4wMDgxYzAuMDA2OSAwIDAtMi42IDAtMi42IDAtMC4wMDc4LTEuMTUgMC0xLjE1IDAtMC4wMDY5IDAtMC4wMDgzIDEuNS0wLjAwODMgMS41LTJlLTMgLTAuMDAxNC0xMS4zLTAuMDAxNC0xMS4zLTAuMDAxNGwtMC4wMDU5Mi0xLjVjMC0wLjAwNzgtMS4xNyAwLjAwMTMtMS4xNyAwLjAwMTN6IiBzdHJva2Utd2lkdGg9Ii45NzUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddAboveIcon {
  background-image: var(--jp-icon-add-above);
}

.jp-AddBelowIcon {
  background-image: var(--jp-icon-add-below);
}

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}

.jp-BellIcon {
  background-image: var(--jp-icon-bell);
}

.jp-BugDotIcon {
  background-image: var(--jp-icon-bug-dot);
}

.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}

.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}

.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}

.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}

.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}

.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}

.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}

.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}

.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}

.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}

.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}

.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}

.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}

.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}

.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}

.jp-CodeCheckIcon {
  background-image: var(--jp-icon-code-check);
}

.jp-CodeIcon {
  background-image: var(--jp-icon-code);
}

.jp-CollapseAllIcon {
  background-image: var(--jp-icon-collapse-all);
}

.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}

.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}

.jp-CopyrightIcon {
  background-image: var(--jp-icon-copyright);
}

.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}

.jp-DeleteIcon {
  background-image: var(--jp-icon-delete);
}

.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}

.jp-DuplicateIcon {
  background-image: var(--jp-icon-duplicate);
}

.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}

.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}

.jp-ErrorIcon {
  background-image: var(--jp-icon-error);
}

.jp-ExpandAllIcon {
  background-image: var(--jp-icon-expand-all);
}

.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}

.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}

.jp-FileIcon {
  background-image: var(--jp-icon-file);
}

.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}

.jp-FilterDotIcon {
  background-image: var(--jp-icon-filter-dot);
}

.jp-FilterIcon {
  background-image: var(--jp-icon-filter);
}

.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}

.jp-FolderFavoriteIcon {
  background-image: var(--jp-icon-folder-favorite);
}

.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}

.jp-HomeIcon {
  background-image: var(--jp-icon-home);
}

.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}

.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}

.jp-InfoIcon {
  background-image: var(--jp-icon-info);
}

.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}

.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}

.jp-JuliaIcon {
  background-image: var(--jp-icon-julia);
}

.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}

.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}

.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}

.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}

.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}

.jp-LaunchIcon {
  background-image: var(--jp-icon-launch);
}

.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}

.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}

.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}

.jp-ListIcon {
  background-image: var(--jp-icon-list);
}

.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}

.jp-MoveDownIcon {
  background-image: var(--jp-icon-move-down);
}

.jp-MoveUpIcon {
  background-image: var(--jp-icon-move-up);
}

.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}

.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}

.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}

.jp-NumberingIcon {
  background-image: var(--jp-icon-numbering);
}

.jp-OfflineBoltIcon {
  background-image: var(--jp-icon-offline-bolt);
}

.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}

.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}

.jp-PdfIcon {
  background-image: var(--jp-icon-pdf);
}

.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}

.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}

.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}

.jp-RedoIcon {
  background-image: var(--jp-icon-redo);
}

.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}

.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}

.jp-RunIcon {
  background-image: var(--jp-icon-run);
}

.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}

.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}

.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}

.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}

.jp-ShareIcon {
  background-image: var(--jp-icon-share);
}

.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}

.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}

.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}

.jp-TableRowsIcon {
  background-image: var(--jp-icon-table-rows);
}

.jp-TagIcon {
  background-image: var(--jp-icon-tag);
}

.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}

.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}

.jp-TocIcon {
  background-image: var(--jp-icon-toc);
}

.jp-TreeViewIcon {
  background-image: var(--jp-icon-tree-view);
}

.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}

.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}

.jp-UserIcon {
  background-image: var(--jp-icon-user);
}

.jp-UsersIcon {
  background-image: var(--jp-icon-users);
}

.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}

.jp-WordIcon {
  background-image: var(--jp-icon-word);
}

.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.lm-TabBar .lm-TabBar-addButton {
  align-items: center;
  display: flex;
  padding: 4px;
  padding-bottom: 5px;
  margin-right: 1px;
  background-color: var(--jp-layout-color2);
}

.lm-TabBar .lm-TabBar-addButton:hover {
  background-color: var(--jp-layout-color1);
}

.lm-DockPanel-tabBar .lm-TabBar-tab {
  width: var(--jp-private-horizontal-tab-width);
}

.lm-DockPanel-tabBar .lm-TabBar-content {
  flex: unset;
}

.lm-DockPanel-tabBar[data-orientation='horizontal'] {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}

/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}

.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}

.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}

.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}

.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}

.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}

.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}

.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}

.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}

/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}

.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}

.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}

.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}

.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}

.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}

.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}

/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

.jp-icon-dot[fill] {
  fill: var(--jp-warn-color0);
}

.jp-jupyter-icon-color[fill] {
  fill: var(--jp-jupyter-icon-color, var(--jp-warn-color0));
}

.jp-notebook-icon-color[fill] {
  fill: var(--jp-notebook-icon-color, var(--jp-warn-color0));
}

.jp-json-icon-color[fill] {
  fill: var(--jp-json-icon-color, var(--jp-warn-color1));
}

.jp-console-icon-color[fill] {
  fill: var(--jp-console-icon-color, white);
}

.jp-console-icon-background-color[fill] {
  fill: var(--jp-console-icon-background-color, var(--jp-brand-color1));
}

.jp-terminal-icon-color[fill] {
  fill: var(--jp-terminal-icon-color, var(--jp-layout-color2));
}

.jp-terminal-icon-background-color[fill] {
  fill: var(
    --jp-terminal-icon-background-color,
    var(--jp-inverse-layout-color2)
  );
}

.jp-text-editor-icon-color[fill] {
  fill: var(--jp-text-editor-icon-color, var(--jp-inverse-layout-color3));
}

.jp-inspector-icon-color[fill] {
  fill: var(--jp-inspector-icon-color, var(--jp-inverse-layout-color3));
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* stylelint-disable selector-max-class, selector-max-compound-selectors */

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}

.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* stylelint-enable selector-max-class, selector-max-compound-selectors */

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) .jp-icon-hoverShow-content {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FormGroup-content fieldset {
  border: none;
  padding: 0;
  min-width: 0;
  width: 100%;
}

/* stylelint-disable selector-max-type */

.jp-FormGroup-content fieldset .jp-inputFieldWrapper input,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper select,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper textarea {
  font-size: var(--jp-content-font-size2);
  border-color: var(--jp-input-border-color);
  border-style: solid;
  border-radius: var(--jp-border-radius);
  border-width: 1px;
  padding: 6px 8px;
  background: none;
  color: var(--jp-ui-font-color0);
  height: inherit;
}

.jp-FormGroup-content fieldset input[type='checkbox'] {
  position: relative;
  top: 2px;
  margin-left: 0;
}

.jp-FormGroup-content button.jp-mod-styled {
  cursor: pointer;
}

.jp-FormGroup-content .checkbox label {
  cursor: pointer;
  font-size: var(--jp-content-font-size1);
}

.jp-FormGroup-content .jp-root > fieldset > legend {
  display: none;
}

.jp-FormGroup-content .jp-root > fieldset > p {
  display: none;
}

/** copy of `input.jp-mod-styled:focus` style */
.jp-FormGroup-content fieldset input:focus,
.jp-FormGroup-content fieldset select:focus {
  -moz-outline-radius: unset;
  outline: var(--jp-border-width) solid var(--md-blue-500);
  outline-offset: -1px;
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-FormGroup-content fieldset input:hover:not(:focus),
.jp-FormGroup-content fieldset select:hover:not(:focus) {
  background-color: var(--jp-border-color2);
}

/* stylelint-enable selector-max-type */

.jp-FormGroup-content .checkbox .field-description {
  /* Disable default description field for checkbox:
   because other widgets do not have description fields,
   we add descriptions to each widget on the field level.
  */
  display: none;
}

.jp-FormGroup-content #root__description {
  display: none;
}

.jp-FormGroup-content .jp-modifiedIndicator {
  width: 5px;
  background-color: var(--jp-brand-color2);
  margin-top: 0;
  margin-left: calc(var(--jp-private-settingeditor-modifier-indent) * -1);
  flex-shrink: 0;
}

.jp-FormGroup-content .jp-modifiedIndicator.jp-errorIndicator {
  background-color: var(--jp-error-color0);
  margin-right: 0.5em;
}

/* RJSF ARRAY style */

.jp-arrayFieldWrapper legend {
  font-size: var(--jp-content-font-size2);
  color: var(--jp-ui-font-color0);
  flex-basis: 100%;
  padding: 4px 0;
  font-weight: var(--jp-content-heading-font-weight);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-arrayFieldWrapper .field-description {
  padding: 4px 0;
  white-space: pre-wrap;
}

.jp-arrayFieldWrapper .array-item {
  width: 100%;
  border: 1px solid var(--jp-border-color2);
  border-radius: 4px;
  margin: 4px;
}

.jp-ArrayOperations {
  display: flex;
  margin-left: 8px;
}

.jp-ArrayOperationsButton {
  margin: 2px;
}

.jp-ArrayOperationsButton .jp-icon3[fill] {
  fill: var(--jp-ui-font-color0);
}

button.jp-ArrayOperationsButton.jp-mod-styled:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

/* RJSF form validation error */

.jp-FormGroup-content .validationErrors {
  color: var(--jp-error-color0);
}

/* Hide panel level error as duplicated the field level error */
.jp-FormGroup-content .panel.errors {
  display: none;
}

/* RJSF normal content (settings-editor) */

.jp-FormGroup-contentNormal {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-FormGroup-contentItem {
  margin-left: 7px;
  color: var(--jp-ui-font-color0);
}

.jp-FormGroup-contentNormal .jp-FormGroup-description {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-default {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-fieldLabel {
  font-size: var(--jp-content-font-size1);
  font-weight: normal;
  min-width: 120px;
}

.jp-FormGroup-contentNormal fieldset:not(:first-child) {
  margin-left: 7px;
}

.jp-FormGroup-contentNormal .field-array-of-string .array-item {
  /* Display `jp-ArrayOperations` buttons side-by-side with content except
    for small screens where flex-wrap will place them one below the other.
  */
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-objectFieldWrapper .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

/* RJSF compact content (metadata-form) */

.jp-FormGroup-content.jp-FormGroup-contentCompact {
  width: 100%;
}

.jp-FormGroup-contentCompact .form-group {
  display: flex;
  padding: 0.5em 0.2em 0.5em 0;
}

.jp-FormGroup-contentCompact
  .jp-FormGroup-compactTitle
  .jp-FormGroup-description {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color2);
}

.jp-FormGroup-contentCompact .jp-FormGroup-fieldLabel {
  padding-bottom: 0.3em;
}

.jp-FormGroup-contentCompact .jp-inputFieldWrapper .form-control {
  width: 100%;
  box-sizing: border-box;
}

.jp-FormGroup-contentCompact .jp-arrayFieldWrapper .jp-FormGroup-compactTitle {
  padding-bottom: 7px;
}

.jp-FormGroup-contentCompact
  .jp-objectFieldWrapper
  .jp-objectFieldWrapper
  .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

.jp-FormGroup-contentCompact ul.error-detail {
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;
  padding-inline-start: 1em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-SidePanel {
  display: flex;
  flex-direction: column;
  min-width: var(--jp-sidebar-min-width);
  overflow-y: auto;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size1);
}

.jp-SidePanel-header {
  flex: 0 0 auto;
  display: flex;
  border-bottom: var(--jp-border-width) solid var(--jp-border-color2);
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin: 0;
  padding: 2px;
  text-transform: uppercase;
}

.jp-SidePanel-toolbar {
  flex: 0 0 auto;
}

.jp-SidePanel-content {
  flex: 1 1 auto;
}

.jp-SidePanel-toolbar,
.jp-AccordionPanel-toolbar {
  height: var(--jp-private-toolbar-height);
}

.jp-SidePanel-toolbar.jp-Toolbar-micro {
  display: none;
}

.lm-AccordionPanel .jp-AccordionPanel-title {
  box-sizing: border-box;
  line-height: 25px;
  margin: 0;
  display: flex;
  align-items: center;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  font-size: var(--jp-ui-font-size0);
}

.jp-AccordionPanel-title {
  cursor: pointer;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  text-transform: uppercase;
}

.lm-AccordionPanel[data-orientation='horizontal'] > .jp-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleLabel {
  user-select: none;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleCollapser {
  transform: rotate(-90deg);
  margin: auto 0;
  height: 16px;
}

.jp-AccordionPanel-title.lm-mod-expanded .lm-AccordionPanel-titleCollapser {
  transform: rotate(0deg);
}

.lm-AccordionPanel .jp-AccordionPanel-toolbar {
  background: none;
  box-shadow: none;
  border: none;
  margin-left: auto;
}

.lm-AccordionPanel .lm-SplitPanel-handle:hover {
  background: var(--jp-layout-color3);
}

.jp-text-truncated {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent::before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent::after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input[type='checkbox'].jp-mod-styled {
  appearance: checkbox;
  -webkit-appearance: checkbox;
  -moz-appearance: checkbox;
  height: auto;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper:not(.multiple) {
  height: 28px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

select.jp-mod-styled:not([multiple]) {
  height: 32px;
}

select.jp-mod-styled[multiple] {
  max-height: 200px;
  overflow-y: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-switch {
  display: flex;
  align-items: center;
  padding-left: 4px;
  padding-right: 4px;
  font-size: var(--jp-ui-font-size1);
  background-color: transparent;
  color: var(--jp-ui-font-color1);
  border: none;
  height: 20px;
}

.jp-switch:hover {
  background-color: var(--jp-layout-color2);
}

.jp-switch-label {
  margin-right: 5px;
  font-family: var(--jp-ui-font-family);
}

.jp-switch-track {
  cursor: pointer;
  background-color: var(--jp-switch-color, var(--jp-border-color1));
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
  height: 16px;
  width: 35px;
  position: relative;
}

.jp-switch-track::before {
  content: '';
  position: absolute;
  height: 10px;
  width: 10px;
  margin: 3px;
  left: 0;
  background-color: var(--jp-ui-inverse-font-color1);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

.jp-switch[aria-checked='true'] .jp-switch-track {
  background-color: var(--jp-switch-true-position-color, var(--jp-warn-color0));
}

.jp-switch[aria-checked='true'] .jp-switch-track::before {
  /* track width (35) - margins (3 + 3) - thumb width (10) */
  left: 19px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 8;
  overflow-x: hidden;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0;
  margin: 0;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0 6px;
  margin: 0;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent > span {
  padding: 0;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar.jp-Toolbar-micro {
  padding: 0;
  min-height: 0;
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar {
  border: none;
  box-shadow: none;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-WindowedPanel-outer {
  position: relative;
  overflow-y: auto;
}

.jp-WindowedPanel-inner {
  position: relative;
}

.jp-WindowedPanel-window {
  position: absolute;
  left: 0;
  right: 0;
  overflow: visible;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

body {
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
}

/* Disable native link decoration styles everywhere outside of dialog boxes */
a {
  text-decoration: unset;
  color: unset;
}

a:hover {
  text-decoration: unset;
  color: unset;
}

/* Accessibility for links inside dialog box text */
.jp-Dialog-content a {
  text-decoration: revert;
  color: var(--jp-content-link-color);
}

.jp-Dialog-content a:hover {
  text-decoration: revert;
}

/* Styles for ui-components */
.jp-Button {
  color: var(--jp-ui-font-color2);
  border-radius: var(--jp-border-radius);
  padding: 0 12px;
  font-size: var(--jp-ui-font-size1);

  /* Copy from blueprint 3 */
  display: inline-flex;
  flex-direction: row;
  border: none;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  text-align: left;
  vertical-align: middle;
  min-height: 30px;
  min-width: 30px;
}

.jp-Button:disabled {
  cursor: not-allowed;
}

.jp-Button:empty {
  padding: 0 !important;
}

.jp-Button.jp-mod-small {
  min-height: 24px;
  min-width: 24px;
  font-size: 12px;
  padding: 0 7px;
}

/* Use our own theme for hover styles */
.jp-Button.jp-mod-minimal:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Button.jp-mod-minimal {
  background: none;
}

.jp-InputGroup {
  display: block;
  position: relative;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border: none;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
  padding-bottom: 0;
  padding-top: 0;
  padding-left: 10px;
  padding-right: 28px;
  position: relative;
  width: 100%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  font-weight: 400;
  height: 30px;
  line-height: 30px;
  outline: none;
  vertical-align: middle;
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input:disabled {
  cursor: not-allowed;
  resize: block;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input:disabled ~ span {
  cursor: not-allowed;
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color2);
}

.jp-InputGroupAction {
  position: absolute;
  bottom: 1px;
  right: 0;
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
  cursor: not-allowed;
  resize: block;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled ~ span {
  cursor: not-allowed;
}

/* Use our own theme for hover and option styles */
/* stylelint-disable-next-line selector-max-type */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}

select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-StatusBar-Widget {
  display: flex;
  align-items: center;
  background: var(--jp-layout-color2);
  min-height: var(--jp-statusbar-height);
  justify-content: space-between;
  padding: 0 10px;
}

.jp-StatusBar-Left {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-StatusBar-Middle {
  display: flex;
  align-items: center;
}

.jp-StatusBar-Right {
  display: flex;
  align-items: center;
  flex-direction: row-reverse;
}

.jp-StatusBar-Item {
  max-height: var(--jp-statusbar-height);
  margin: 0 2px;
  height: var(--jp-statusbar-height);
  white-space: nowrap;
  text-overflow: ellipsis;
  color: var(--jp-ui-font-color1);
  padding: 0 6px;
}

.jp-mod-highlighted:hover {
  background-color: var(--jp-layout-color3);
}

.jp-mod-clicked {
  background-color: var(--jp-brand-color1);
}

.jp-mod-clicked:hover {
  background-color: var(--jp-brand-color0);
}

.jp-mod-clicked .jp-StatusBar-TextItem {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-StatusBar-HoverItem {
  box-shadow: '0px 4px 4px rgba(0, 0, 0, 0.25)';
}

.jp-StatusBar-TextItem {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  line-height: 24px;
  color: var(--jp-ui-font-color1);
}

.jp-StatusBar-GroupItem {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-Statusbar-ProgressCircle svg {
  display: block;
  margin: 0 auto;
  width: 16px;
  height: 24px;
  align-self: normal;
}

.jp-Statusbar-ProgressCircle path {
  fill: var(--jp-inverse-layout-color3);
}

.jp-Statusbar-ProgressBar-progress-bar {
  height: 10px;
  width: 100px;
  border: solid 0.25px var(--jp-brand-color2);
  border-radius: 3px;
  overflow: hidden;
  align-self: center;
}

.jp-Statusbar-ProgressBar-progress-bar > div {
  background-color: var(--jp-brand-color2);
  background-image: linear-gradient(
    -45deg,
    rgba(255, 255, 255, 0.2) 25%,
    transparent 25%,
    transparent 50%,
    rgba(255, 255, 255, 0.2) 50%,
    rgba(255, 255, 255, 0.2) 75%,
    transparent 75%,
    transparent
  );
  background-size: 40px 40px;
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 14px;
  color: #fff;
  text-align: center;
  animation: jp-Statusbar-ExecutionTime-progress-bar 2s linear infinite;
}

.jp-Statusbar-ProgressBar-progress-bar p {
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  line-height: 10px;
  width: 100px;
}

@keyframes jp-Statusbar-ExecutionTime-progress-bar {
  0% {
    background-position: 0 0;
  }

  100% {
    background-position: 40px 40px;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Modal variant
|----------------------------------------------------------------------------*/

.jp-ModalCommandPalette {
  position: absolute;
  z-index: 10000;
  top: 38px;
  left: 30%;
  margin: 0;
  padding: 4px;
  width: 40%;
  box-shadow: var(--jp-elevation-z4);
  border-radius: 4px;
  background: var(--jp-layout-color0);
}

.jp-ModalCommandPalette .lm-CommandPalette {
  max-height: 40vh;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-close-icon::after {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-header {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-item {
  margin-left: 4px;
  margin-right: 4px;
}

.jp-ModalCommandPalette
  .lm-CommandPalette
  .lm-CommandPalette-item.lm-mod-disabled {
  display: none;
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-SearchIconGroup {
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  padding: 5px 5px 1px;
}

.jp-SearchIconGroup svg {
  height: 20px;
  width: 20px;
}

.jp-SearchIconGroup .jp-icon3[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color2);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item.lm-mod-active {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item.lm-mod-active .lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-inverse-font-color0);
}

.lm-CommandPalette-item.lm-mod-active .jp-icon-selectable[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.6;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty::after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px 24px 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
  resize: both;
}

.jp-Dialog-content.jp-Dialog-content-small {
  max-width: 500px;
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus {
  outline: 1px solid var(--jp-accept-color-normal, var(--jp-brand-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus {
  outline: 1px solid var(--jp-warn-color-normal, var(--jp-error-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline: 1px solid var(--jp-reject-color-normal, var(--md-grey-600));
}

button.jp-Dialog-close-button {
  padding: 0;
  height: 100%;
  min-width: unset;
  min-height: unset;
}

.jp-Dialog-header {
  display: flex;
  justify-content: space-between;
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color1);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-checkbox {
  padding-right: 5px;
}

.jp-Dialog-checkbox > input:focus-visible {
  outline: 1px solid var(--jp-input-active-border-color);
  outline-offset: 1px;
}

.jp-Dialog-spacer {
  flex: 1 1 auto;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Input-Boolean-Dialog {
  flex-direction: row-reverse;
  align-items: end;
  width: 100%;
}

.jp-Input-Boolean-Dialog > label {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error {
  padding: 6px;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error > pre {
  width: auto;
  padding: 10px;
  background: var(--jp-error-color3);
  border: var(--jp-border-width) solid var(--jp-error-color1);
  border-radius: var(--jp-border-radius);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  white-space: pre-wrap;
  word-wrap: break-word;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;
  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;
  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #a0f;
  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;
  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;
  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;
  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;
  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;
  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;
  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;
  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;
  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;
  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ff0;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;
  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;
  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;
  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;
  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;
  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;
  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

:root {
  /* This is the padding value to fill the gaps between lines containing spans with background color. */
  --jp-private-code-span-padding: calc(
    (var(--jp-code-line-height) - 1) * var(--jp-code-font-size) / 2
  );
}

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0;
  padding: 0;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}

.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}

.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}

.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}

.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}

.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}

.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}

.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}

.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}

.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}

.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}

.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}

.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}

.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}

.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}

.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}

.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);

  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

/* stylelint-disable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0;
}

/* stylelint-enable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  table-layout: fixed;
  margin-left: auto;
  margin-bottom: 1em;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}

[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}

.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}

.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}

.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}

.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}

.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}

.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}

.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}

.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: var(--jp-ui-font-size0);
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-cursor-backdrop {
  position: fixed;
  width: 200px;
  height: 200px;
  margin-top: -100px;
  margin-left: -100px;
  will-change: transform;
  z-index: 100;
}

.lm-mod-drag-image {
  will-change: transform;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-lineFormSearch {
  padding: 4px 12px;
  background-color: var(--jp-layout-color2);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
  font-size: var(--jp-ui-font-size1);
}

.jp-lineFormCaption {
  font-size: var(--jp-ui-font-size0);
  line-height: var(--jp-ui-font-size1);
  margin-top: 4px;
  color: var(--jp-ui-font-color0);
}

.jp-baseLineForm {
  border: none;
  border-radius: 0;
  position: absolute;
  background-size: 16px;
  background-repeat: no-repeat;
  background-position: center;
  outline: none;
}

.jp-lineFormButtonContainer {
  top: 4px;
  right: 8px;
  height: 24px;
  padding: 0 12px;
  width: 12px;
}

.jp-lineFormButtonIcon {
  top: 0;
  right: 0;
  background-color: var(--jp-brand-color1);
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  padding: 4px 6px;
}

.jp-lineFormButton {
  top: 0;
  right: 0;
  background-color: transparent;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}

.jp-lineFormWrapper {
  overflow: hidden;
  padding: 0 8px;
  border: 1px solid var(--jp-border-color0);
  background-color: var(--jp-input-active-background);
  height: 22px;
}

.jp-lineFormWrapperFocusWithin {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-lineFormInput {
  background: transparent;
  width: 200px;
  height: 100%;
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  line-height: 28px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/
.jp-DocumentSearch-input {
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  font-size: var(--jp-ui-font-size1);
  background-color: var(--jp-layout-color0);
  font-family: var(--jp-ui-font-family);
  padding: 2px 1px;
  resize: none;
}

.jp-DocumentSearch-overlay {
  position: absolute;
  background-color: var(--jp-toolbar-background);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  border-left: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  top: 0;
  right: 0;
  z-index: 7;
  min-width: 405px;
  padding: 2px;
  font-size: var(--jp-ui-font-size1);

  --jp-private-document-search-button-height: 20px;
}

.jp-DocumentSearch-overlay button {
  background-color: var(--jp-toolbar-background);
  outline: 0;
}

.jp-DocumentSearch-overlay button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-overlay button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-overlay-row {
  display: flex;
  align-items: center;
  margin-bottom: 2px;
}

.jp-DocumentSearch-button-content {
  display: inline-block;
  cursor: pointer;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-button-content svg {
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-input-wrapper {
  border: var(--jp-border-width) solid var(--jp-border-color0);
  display: flex;
  background-color: var(--jp-layout-color0);
  margin: 2px;
}

.jp-DocumentSearch-input-wrapper:focus-within {
  border-color: var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper {
  all: initial;
  overflow: hidden;
  display: inline-block;
  border: none;
  box-sizing: border-box;
}

.jp-DocumentSearch-toggle-wrapper {
  width: 14px;
  height: 14px;
}

.jp-DocumentSearch-button-wrapper {
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
}

.jp-DocumentSearch-toggle-wrapper:focus,
.jp-DocumentSearch-button-wrapper:focus {
  outline: var(--jp-border-width) solid
    var(--jp-cell-editor-active-border-color);
  outline-offset: -1px;
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper,
.jp-DocumentSearch-button-content:focus {
  outline: none;
}

.jp-DocumentSearch-toggle-placeholder {
  width: 5px;
}

.jp-DocumentSearch-input-button::before {
  display: block;
  padding-top: 100%;
}

.jp-DocumentSearch-input-button-off {
  opacity: var(--jp-search-toggle-off-opacity);
}

.jp-DocumentSearch-input-button-off:hover {
  opacity: var(--jp-search-toggle-hover-opacity);
}

.jp-DocumentSearch-input-button-on {
  opacity: var(--jp-search-toggle-on-opacity);
}

.jp-DocumentSearch-index-counter {
  padding-left: 10px;
  padding-right: 10px;
  user-select: none;
  min-width: 35px;
  display: inline-block;
}

.jp-DocumentSearch-up-down-wrapper {
  display: inline-block;
  padding-right: 2px;
  margin-left: auto;
  white-space: nowrap;
}

.jp-DocumentSearch-spacer {
  margin-left: auto;
}

.jp-DocumentSearch-up-down-wrapper button {
  outline: 0;
  border: none;
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
  vertical-align: middle;
  margin: 1px 5px 2px;
}

.jp-DocumentSearch-up-down-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-up-down-button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-filter-button {
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-filter-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled:hover {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-search-options {
  padding: 0 8px;
  margin-left: 3px;
  width: 100%;
  display: grid;
  justify-content: start;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  justify-items: stretch;
}

.jp-DocumentSearch-search-filter-disabled {
  color: var(--jp-ui-font-color2);
}

.jp-DocumentSearch-search-filter {
  display: flex;
  align-items: center;
  user-select: none;
}

.jp-DocumentSearch-regex-error {
  color: var(--jp-error-color0);
}

.jp-DocumentSearch-replace-button-wrapper {
  overflow: hidden;
  display: inline-block;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color0);
  margin: auto 2px;
  padding: 1px 4px;
  height: calc(var(--jp-private-document-search-button-height) + 2px);
}

.jp-DocumentSearch-replace-button-wrapper:focus {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-replace-button {
  display: inline-block;
  text-align: center;
  cursor: pointer;
  box-sizing: border-box;
  color: var(--jp-ui-font-color1);

  /* height - 2 * (padding of wrapper) */
  line-height: calc(var(--jp-private-document-search-button-height) - 2px);
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-replace-button:focus {
  outline: none;
}

.jp-DocumentSearch-replace-wrapper-class {
  margin-left: 14px;
  display: flex;
}

.jp-DocumentSearch-replace-toggle {
  border: none;
  background-color: var(--jp-toolbar-background);
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-replace-toggle:hover {
  background-color: var(--jp-layout-color2);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.cm-editor {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;

  /* Changed to auto to autogrow */
}

.cm-editor pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .cm-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

.jp-CodeMirrorEditor {
  cursor: text;
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.cm-editor.jp-mod-readOnly .cm-cursor {
  display: none;
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.cm-searching,
.cm-searching span {
  /* `.cm-searching span`: we need to override syntax highlighting */
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.cm-searching::selection,
.cm-searching span::selection {
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.jp-current-match > .cm-searching,
.jp-current-match > .cm-searching span,
.cm-searching > .jp-current-match,
.cm-searching > .jp-current-match span {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.jp-current-match > .cm-searching::selection,
.cm-searching > .jp-current-match::selection,
.jp-current-match > .cm-searching span::selection {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.cm-trailingspace {
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAFCAYAAAB4ka1VAAAAsElEQVQIHQGlAFr/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA7+r3zKmT0/+pk9P/7+r3zAAAAAAAAAAABAAAAAAAAAAA6OPzM+/q9wAAAAAA6OPzMwAAAAAAAAAAAgAAAAAAAAAAGR8NiRQaCgAZIA0AGR8NiQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQyoYJ/SY80UAAAAASUVORK5CYII=);
  background-position: center left;
  background-repeat: repeat-x;
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/* Styles for shared cursors (remote cursor locations and selected ranges) */
.jp-CodeMirrorEditor .cm-ySelectionCaret {
  position: relative;
  border-left: 1px solid black;
  margin-left: -1px;
  margin-right: -1px;
  box-sizing: border-box;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret > .cm-ySelectionInfo {
  white-space: nowrap;
  position: absolute;
  top: -1.15em;
  padding-bottom: 0.05em;
  left: -1px;
  font-size: 0.95em;
  font-family: var(--jp-ui-font-family);
  font-weight: bold;
  line-height: normal;
  user-select: none;
  color: white;
  padding-left: 2px;
  padding-right: 2px;
  z-index: 101;
  transition: opacity 0.3s ease-in-out;
}

.jp-CodeMirrorEditor .cm-ySelectionInfo {
  transition-delay: 0.7s;
  opacity: 0;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret:hover > .cm-ySelectionInfo {
  opacity: 1;
  transition-delay: 0s;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser .jp-SidePanel-content {
  display: flex;
  flex-direction: column;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  flex-wrap: wrap;
  row-gap: 12px;
  border-bottom: none;
  height: auto;
  margin: 8px 12px 0;
  box-shadow: none;
  padding: 0;
  justify-content: flex-start;
}

.jp-FileBrowser-Panel {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 8px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0 2px;
  padding: 0 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  padding-left: 0;
  padding-right: 2px;
  align-items: center;
  height: unset;
}

.jp-FileBrowser-toolbar > .jp-Toolbar-item .jp-ToolbarButtonComponent {
  width: 40px;
}

/*-----------------------------------------------------------------------------
| Other styles
|----------------------------------------------------------------------------*/

.jp-FileDialog.jp-mod-conflict input {
  color: var(--jp-error-color1);
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

.jp-LastModified-hidden {
  display: none;
}

.jp-FileSize-hidden {
  display: none;
}

.jp-FileBrowser .lm-AccordionPanel > h3:first-child {
  display: none;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-DirListing-headerItem.jp-id-filesize {
  flex: 0 0 75px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-id-narrow {
  display: none;
  flex: 0 0 5px;
  padding: 4px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
  color: var(--jp-border-color2);
}

.jp-DirListing-narrow .jp-id-narrow {
  display: block;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-content mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.jp-DirListing-content .jp-DirListing-item.jp-mod-selected mark {
  color: var(--jp-ui-inverse-font-color0);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-checkboxWrapper {
  /* Increases hit area of checkbox. */
  padding: 4px;
}

.jp-DirListing-header
  .jp-DirListing-checkboxWrapper
  + .jp-DirListing-headerItem {
  padding-left: 4px;
}

.jp-DirListing-content .jp-DirListing-checkboxWrapper {
  position: relative;
  left: -4px;
  margin: -4px 0 -4px -8px;
}

.jp-DirListing-checkboxWrapper.jp-mod-visible {
  visibility: visible;
}

/* For devices that support hovering, hide checkboxes until hovered, selected...
*/
@media (hover: hover) {
  .jp-DirListing-checkboxWrapper {
    visibility: hidden;
  }

  .jp-DirListing-item:hover .jp-DirListing-checkboxWrapper,
  .jp-DirListing-item.jp-mod-selected .jp-DirListing-checkboxWrapper {
    visibility: visible;
  }
}

.jp-DirListing-item[data-is-dot] {
  opacity: 75%;
}

.jp-DirListing-item.jp-mod-selected {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemText:focus {
  outline-width: 2px;
  outline-color: var(--jp-inverse-layout-color1);
  outline-style: solid;
  outline-offset: 1px;
}

.jp-DirListing-item.jp-mod-selected .jp-DirListing-itemText:focus {
  outline-color: var(--jp-layout-color1);
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-itemFileSize {
  flex: 0 0 90px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon::before {
  color: var(--jp-success-color1);
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.jp-mod-running.jp-mod-selected
  .jp-DirListing-itemIcon::before {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-OutputPrompt {
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-OutputArea-prompt {
  display: table-cell;
  vertical-align: top;
}

.jp-OutputArea-output {
  display: table-cell;
  width: 100%;
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea .jp-RenderedText {
  padding-left: 1ch;
}

/**
 * Prompt overlay.
 */

.jp-OutputArea-promptOverlay {
  position: absolute;
  top: 0;
  width: var(--jp-cell-prompt-width);
  height: 100%;
  opacity: 0.5;
}

.jp-OutputArea-promptOverlay:hover {
  background: var(--jp-layout-color2);
  box-shadow: inset 0 0 1px var(--jp-inverse-layout-color0);
  cursor: zoom-out;
}

.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay:hover {
  cursor: zoom-in;
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0;
  padding: 0;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

.jp-TrimmedOutputs pre {
  background: var(--jp-layout-color3);
  font-size: calc(var(--jp-code-font-size) * 1.4);
  text-align: center;
  text-transform: uppercase;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/* Hide empty lines in the output area, for instance due to cleared widgets */
.jp-OutputArea-prompt:empty {
  padding: 0;
  border: 0;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0;
  width: 100%;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
  border-top: var(--jp-border-width) solid transparent;
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;

  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;

  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0 0.25em;
  margin: 0 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input::placeholder {
  opacity: 0;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

.jp-Stdin-input:focus::placeholder {
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

@media print {
  .jp-OutputArea-child {
    break-inside: avoid-page;
  }
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-OutputPrompt {
    display: table-row;
    text-align: left;
  }

  .jp-OutputArea-child .jp-OutputArea-output {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }
}

/* Trimmed outputs warning */
.jp-TrimmedOutputs > a {
  margin: 10px;
  text-decoration: none;
  cursor: pointer;
}

.jp-TrimmedOutputs > a:hover {
  text-decoration: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Table of Contents
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toc-active-width: 4px;
}

.jp-TableOfContents {
  display: flex;
  flex-direction: column;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  height: 100%;
}

.jp-TableOfContents-placeholder {
  text-align: center;
}

.jp-TableOfContents-placeholderContent {
  color: var(--jp-content-font-color2);
  padding: 8px;
}

.jp-TableOfContents-placeholderContent > h3 {
  margin-bottom: var(--jp-content-heading-margin-bottom);
}

.jp-TableOfContents .jp-SidePanel-content {
  overflow-y: auto;
}

.jp-TableOfContents-tree {
  margin: 4px;
}

.jp-TableOfContents ol {
  list-style-type: none;
}

/* stylelint-disable-next-line selector-max-type */
.jp-TableOfContents li > ol {
  /* Align left border with triangle icon center */
  padding-left: 11px;
}

.jp-TableOfContents-content {
  /* left margin for the active heading indicator */
  margin: 0 0 0 var(--jp-private-toc-active-width);
  padding: 0;
  background-color: var(--jp-layout-color1);
}

.jp-tocItem {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-tocItem-heading {
  display: flex;
  cursor: pointer;
}

.jp-tocItem-heading:hover {
  background-color: var(--jp-layout-color2);
}

.jp-tocItem-content {
  display: block;
  padding: 4px 0;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow-x: hidden;
}

.jp-tocItem-collapser {
  height: 20px;
  margin: 2px 2px 0;
  padding: 0;
  background: none;
  border: none;
  cursor: pointer;
}

.jp-tocItem-collapser:hover {
  background-color: var(--jp-layout-color3);
}

/* Active heading indicator */

.jp-tocItem-heading::before {
  content: ' ';
  background: transparent;
  width: var(--jp-private-toc-active-width);
  height: 24px;
  position: absolute;
  left: 0;
  border-radius: var(--jp-border-radius);
}

.jp-tocItem-heading.jp-tocItem-active::before {
  background-color: var(--jp-brand-color1);
}

.jp-tocItem-heading:hover.jp-tocItem-active::before {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;

  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0;
  bottom: 0;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Hiding collapsers in print mode.

Note: input and output wrappers have "display: block" propery in print mode.
*/

@media print {
  .jp-Collapser {
    display: none;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0;
  width: 100%;
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-InputArea-editor {
  display: table-cell;
  overflow: hidden;
  vertical-align: top;

  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  background: var(--jp-cell-editor-background);
}

.jp-InputPrompt {
  display: table-cell;
  vertical-align: top;
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-InputArea-editor {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }

  .jp-InputPrompt {
    display: table-row;
    text-align: left;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: table;
  table-layout: fixed;
  width: 100%;
}

.jp-Placeholder-prompt {
  display: table-cell;
  box-sizing: border-box;
}

.jp-Placeholder-content {
  display: table-cell;
  padding: 4px 6px;
  border: 1px solid transparent;
  border-radius: 0;
  background: none;
  box-sizing: border-box;
  cursor: pointer;
}

.jp-Placeholder-contentContainer {
  display: flex;
}

.jp-Placeholder-content:hover,
.jp-InputPlaceholder > .jp-Placeholder-content:hover {
  border-color: var(--jp-layout-color3);
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

.jp-PlaceholderText {
  white-space: nowrap;
  overflow-x: hidden;
  color: var(--jp-inverse-layout-color3);
  font-family: var(--jp-code-font-family);
}

.jp-InputPlaceholder > .jp-Placeholder-content {
  border-color: var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0;
  margin: 0;

  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 24em;
  margin-left: var(--jp-private-cell-scrolling-output-offset);
  resize: vertical;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea[style*='height'] {
  max-height: unset;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea::after {
  content: ' ';
  box-shadow: inset 0 0 6px 2px rgb(0 0 0 / 30%);
  width: 100%;
  height: 100%;
  position: sticky;
  bottom: 0;
  top: 0;
  margin-top: -50%;
  float: left;
  display: block;
  pointer-events: none;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-child {
  padding-top: 6px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  width: calc(
    var(--jp-cell-prompt-width) - var(--jp-private-cell-scrolling-output-offset)
  );
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay {
  left: calc(-1 * var(--jp-private-cell-scrolling-output-offset));
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  display: table-cell;
  width: 100%;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

/* collapseHeadingButton (show always if hiddenCellsButton is _not_ shown) */
.jp-collapseHeadingButton {
  display: flex;
  min-height: var(--jp-cell-collapser-min-height);
  font-size: var(--jp-code-font-size);
  position: absolute;
  background-color: transparent;
  background-size: 25px;
  background-repeat: no-repeat;
  background-position-x: center;
  background-position-y: top;
  background-image: var(--jp-icon-caret-down);
  right: 0;
  top: 0;
  bottom: 0;
}

.jp-collapseHeadingButton.jp-mod-collapsed {
  background-image: var(--jp-icon-caret-right);
}

/*
 set the container font size to match that of content
 so that the nested collapse buttons have the right size
*/
.jp-MarkdownCell .jp-InputPrompt {
  font-size: var(--jp-content-font-size1);
}

/*
  Align collapseHeadingButton with cell top header
  The font sizes are identical to the ones in packages/rendermime/style/base.css
*/
.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='1'] {
  font-size: var(--jp-content-font-size5);
  background-position-y: calc(0.3 * var(--jp-content-font-size5));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='2'] {
  font-size: var(--jp-content-font-size4);
  background-position-y: calc(0.3 * var(--jp-content-font-size4));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='3'] {
  font-size: var(--jp-content-font-size3);
  background-position-y: calc(0.3 * var(--jp-content-font-size3));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='4'] {
  font-size: var(--jp-content-font-size2);
  background-position-y: calc(0.3 * var(--jp-content-font-size2));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='5'] {
  font-size: var(--jp-content-font-size1);
  background-position-y: top;
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='6'] {
  font-size: var(--jp-content-font-size0);
  background-position-y: top;
}

/* collapseHeadingButton (show only on (hover,active) if hiddenCellsButton is shown) */
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-collapseHeadingButton {
  display: none;
}

.jp-Notebook.jp-mod-showHiddenCellsButton
  :is(.jp-MarkdownCell:hover, .jp-mod-active)
  .jp-collapseHeadingButton {
  display: flex;
}

/* showHiddenCellsButton (only show if jp-mod-showHiddenCellsButton is set, which
is a consequence of the showHiddenCellsButton option in Notebook Settings)*/
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton {
  margin-left: calc(var(--jp-cell-prompt-width) + 2 * var(--jp-code-padding));
  margin-top: var(--jp-code-padding);
  border: 1px solid var(--jp-border-color2);
  background-color: var(--jp-border-color3) !important;
  color: var(--jp-content-font-color0) !important;
  display: flex;
}

.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton:hover {
  background-color: var(--jp-border-color2) !important;
}

.jp-showHiddenCellsButton {
  display: none;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Using block instead of flex to allow the use of the break-inside CSS property for
cell outputs.
*/

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-notebook-toolbar-padding: 2px 5px 2px 2px;
}

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: var(--jp-notebook-toolbar-padding);

  /* disable paint containment from lumino 2.0 default strict CSS containment */
  contain: style size !important;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

.jp-Toolbar-responsive-popup {
  position: absolute;
  height: fit-content;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: var(--jp-notebook-toolbar-padding);
  z-index: 1;
  right: 0;
  top: 0;
}

.jp-Toolbar > .jp-Toolbar-responsive-opener {
  margin-left: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-Notebook-ExecutionIndicator {
  position: relative;
  display: inline-block;
  height: 100%;
  z-index: 9997;
}

.jp-Notebook-ExecutionIndicator-tooltip {
  visibility: hidden;
  height: auto;
  width: max-content;
  width: -moz-max-content;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color1);
  text-align: justify;
  border-radius: 6px;
  padding: 0 5px;
  position: fixed;
  display: table;
}

.jp-Notebook-ExecutionIndicator-tooltip.up {
  transform: translateX(-50%) translateY(-100%) translateY(-32px);
}

.jp-Notebook-ExecutionIndicator-tooltip.down {
  transform: translateX(calc(-100% + 16px)) translateY(5px);
}

.jp-Notebook-ExecutionIndicator-tooltip.hidden {
  display: none;
}

.jp-Notebook-ExecutionIndicator:hover .jp-Notebook-ExecutionIndicator-tooltip {
  visibility: visible;
}

.jp-Notebook-ExecutionIndicator span {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  color: var(--jp-ui-font-color1);
  line-height: 24px;
  display: block;
}

.jp-Notebook-ExecutionIndicator-progress-bar {
  display: flex;
  justify-content: center;
  height: 100%;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*
 * Execution indicator
 */
.jp-tocItem-content::after {
  content: '';

  /* Must be identical to form a circle */
  width: 12px;
  height: 12px;
  background: none;
  border: none;
  position: absolute;
  right: 0;
}

.jp-tocItem-content[data-running='0']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background: none;
}

.jp-tocItem-content[data-running='1']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background-color: var(--jp-inverse-layout-color3);
}

.jp-tocItem-content[data-running='0'],
.jp-tocItem-content[data-running='1'] {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Notebook-footer {
  height: 27px;
  margin-left: calc(
    var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
      var(--jp-cell-padding)
  );
  width: calc(
    100% -
      (
        var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
          var(--jp-cell-padding) + var(--jp-cell-padding)
      )
  );
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  color: var(--jp-ui-font-color3);
  margin-top: 6px;
  background: none;
  cursor: pointer;
}

.jp-Notebook-footer:focus {
  border-color: var(--jp-cell-editor-active-border-color);
}

/* For devices that support hovering, hide footer until hover */
@media (hover: hover) {
  .jp-Notebook-footer {
    opacity: 0;
  }

  .jp-Notebook-footer:focus,
  .jp-Notebook-footer:hover {
    opacity: 1;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-side-by-side-output-size: 1fr;
  --jp-side-by-side-resized-cell: var(--jp-side-by-side-output-size);
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

/* stylelint-disable selector-max-class */

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-MainAreaWidget-ContainStrict .jp-Notebook * {
  contain: strict;
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* cell is dirty */
.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt {
  color: var(--jp-warn-color1);
}

.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt::before {
  color: var(--jp-warn-color1);
  content: '•';
}

.jp-Notebook .jp-Cell.jp-mod-active.jp-mod-dirty .jp-Collapser {
  background: var(--jp-warn-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: block;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-ActiveCellTool {
  padding: 12px 0;
  display: flex;
}

.jp-ActiveCellTool-Content {
  flex: 1 1 auto;
}

.jp-ActiveCellTool .jp-ActiveCellTool-CellContent {
  background: var(--jp-cell-editor-background);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  min-height: 29px;
}

.jp-ActiveCellTool .jp-InputPrompt {
  min-width: calc(var(--jp-cell-prompt-width) * 0.75);
}

.jp-ActiveCellTool-CellContent > pre {
  padding: 5px 4px;
  margin: 0;
  white-space: normal;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label,
.jp-NumberSetter label {
  line-height: 1.4;
}

.jp-NotebookTools .jp-select-wrapper {
  margin-top: 4px;
  margin-bottom: 0;
}

.jp-NumberSetter input {
  width: 100%;
  margin-top: 4px;
}

.jp-NotebookTools .jp-Collapse {
  margin-top: 16px;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Side-by-side Mode (.jp-mod-sideBySide)
|----------------------------------------------------------------------------*/
.jp-mod-sideBySide.jp-Notebook .jp-Notebook-cell {
  margin-top: 3em;
  margin-bottom: 3em;
  margin-left: 5%;
  margin-right: 5%;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell {
  display: grid;
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-output-size)
    );
  grid-template-rows: auto minmax(0, 1fr) auto;
  grid-template-areas:
    'header header header'
    'input handle output'
    'footer footer footer';
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell.jp-mod-resizedCell {
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-resized-cell)
    );
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellHeader {
  grid-area: header;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-inputWrapper {
  grid-area: input;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-outputWrapper {
  /* overwrite the default margin (no vertical separation needed in side by side move */
  margin-top: 0;
  grid-area: output;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellFooter {
  grid-area: footer;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle {
  grid-area: handle;
  user-select: none;
  display: block;
  height: 100%;
  cursor: ew-resize;
  padding: 0 var(--jp-cell-padding);
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle::after {
  content: '';
  display: block;
  background: var(--jp-border-color2);
  height: 100%;
  width: 5px;
}

.jp-mod-sideBySide.jp-Notebook
  .jp-CodeCell.jp-mod-resizedCell
  .jp-CellResizeHandle::after {
  background: var(--jp-border-color0);
}

.jp-CellResizeHandle {
  display: none;
}

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Cell-Placeholder {
  padding-left: 55px;
}

.jp-Cell-Placeholder-wrapper {
  background: #fff;
  border: 1px solid;
  border-color: #e5e6e9 #dfe0e4 #d0d1d5;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  margin: 10px 15px;
}

.jp-Cell-Placeholder-wrapper-inner {
  padding: 15px;
  position: relative;
}

.jp-Cell-Placeholder-wrapper-body {
  background-repeat: repeat;
  background-size: 50% auto;
}

.jp-Cell-Placeholder-wrapper-body div {
  background: #f6f7f8;
  background-image: -webkit-linear-gradient(
    left,
    #f6f7f8 0%,
    #edeef1 20%,
    #f6f7f8 40%,
    #f6f7f8 100%
  );
  background-repeat: no-repeat;
  background-size: 800px 104px;
  height: 104px;
  position: absolute;
  right: 15px;
  left: 15px;
  top: 15px;
}

div.jp-Cell-Placeholder-h1 {
  top: 20px;
  height: 20px;
  left: 15px;
  width: 150px;
}

div.jp-Cell-Placeholder-h2 {
  left: 15px;
  top: 50px;
  height: 10px;
  width: 100px;
}

div.jp-Cell-Placeholder-content-1,
div.jp-Cell-Placeholder-content-2,
div.jp-Cell-Placeholder-content-3 {
  left: 15px;
  right: 15px;
  height: 10px;
}

div.jp-Cell-Placeholder-content-1 {
  top: 100px;
}

div.jp-Cell-Placeholder-content-2 {
  top: 120px;
}

div.jp-Cell-Placeholder-content-3 {
  top: 140px;
}

</style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0 2px 1px -1px var(--jp-shadow-umbra-color),
    0 1px 1px 0 var(--jp-shadow-penumbra-color),
    0 1px 3px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0 3px 1px -2px var(--jp-shadow-umbra-color),
    0 2px 2px 0 var(--jp-shadow-penumbra-color),
    0 1px 5px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0 2px 4px -1px var(--jp-shadow-umbra-color),
    0 4px 5px 0 var(--jp-shadow-penumbra-color),
    0 1px 10px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0 3px 5px -1px var(--jp-shadow-umbra-color),
    0 6px 10px 0 var(--jp-shadow-penumbra-color),
    0 1px 18px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0 5px 5px -3px var(--jp-shadow-umbra-color),
    0 8px 10px 1px var(--jp-shadow-penumbra-color),
    0 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0 7px 8px -4px var(--jp-shadow-umbra-color),
    0 12px 17px 2px var(--jp-shadow-penumbra-color),
    0 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0 8px 10px -5px var(--jp-shadow-umbra-color),
    0 16px 24px 2px var(--jp-shadow-penumbra-color),
    0 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0 10px 13px -6px var(--jp-shadow-umbra-color),
    0 20px 31px 3px var(--jp-shadow-penumbra-color),
    0 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0 11px 15px -7px var(--jp-shadow-umbra-color),
    0 24px 38px 3px var(--jp-shadow-penumbra-color),
    0 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-inverse-border-color: var(--md-grey-600);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;
  --jp-ui-font-family: system-ui, -apple-system, blinkmacsystemfont, 'Segoe UI',
    helvetica, arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;
  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);
  --jp-content-link-color: var(--md-blue-900);
  --jp-content-font-family: system-ui, -apple-system, blinkmacsystemfont,
    'Segoe UI', helvetica, arial, sans-serif, 'Apple Color Emoji',
    'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: menlo, consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-900);
  --jp-brand-color1: var(--md-blue-700);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);
  --jp-accent-color0: var(--md-green-900);
  --jp-accent-color1: var(--md-green-700);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-900);
  --jp-warn-color1: var(--md-orange-700);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);
  --jp-error-color0: var(--md-red-900);
  --jp-error-color1: var(--md-red-700);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);
  --jp-success-color0: var(--md-green-900);
  --jp-success-color1: var(--md-green-700);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);
  --jp-info-color0: var(--md-cyan-900);
  --jp-info-color1: var(--md-cyan-700);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;
  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;
  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);
  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: var(--jp-code-font-family-default);
  --jp-cell-prompt-letter-spacing: 0;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);

  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;

  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Statusbar specific styles */

  --jp-statusbar-height: 24px;

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-inverse-border-color);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: rgb(0, 54, 109);
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #a2f;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #a2f;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /*
    RTC user specific colors.
    These colors are used for the cursor, username in the editor,
    and the icon of the user.
  */

  --jp-collaborator-color1: #ffad8e;
  --jp-collaborator-color2: #dac83d;
  --jp-collaborator-color3: #72dd76;
  --jp-collaborator-color4: #00e4d0;
  --jp-collaborator-color5: #45d4ff;
  --jp-collaborator-color6: #e2b1ff;
  --jp-collaborator-color7: #ff9de6;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 250px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);

  /* Button colors */
  --jp-accept-color-normal: var(--md-blue-700);
  --jp-accept-color-hover: var(--md-blue-800);
  --jp-accept-color-active: var(--md-blue-900);
  --jp-warn-color-normal: var(--md-red-700);
  --jp-warn-color-hover: var(--md-red-800);
  --jp-warn-color-active: var(--md-red-900);
  --jp-reject-color-normal: var(--md-grey-600);
  --jp-reject-color-hover: var(--md-grey-700);
  --jp-reject-color-active: var(--md-grey-800);

  /* File or activity icons and switch semantic variables */
  --jp-jupyter-icon-color: #f37626;
  --jp-notebook-icon-color: #f37626;
  --jp-json-icon-color: var(--md-orange-700);
  --jp-console-icon-background-color: var(--md-blue-700);
  --jp-console-icon-color: white;
  --jp-terminal-icon-background-color: var(--md-grey-800);
  --jp-terminal-icon-color: var(--md-grey-200);
  --jp-text-editor-icon-color: var(--md-grey-700);
  --jp-inspector-icon-color: var(--md-grey-700);
  --jp-switch-color: var(--md-grey-400);
  --jp-switch-true-position-color: var(--md-orange-900);
}
</style>
<style type="text/css">
/* Force rendering true colors when outputing to pdf */
* {
  -webkit-print-color-adjust: exact;
}

/* Misc */
a.anchor-link {
  display: none;
}

/* Input area styling */
.jp-InputArea {
  overflow: hidden;
}

.jp-InputArea-editor {
  overflow: hidden;
}

.cm-editor.cm-s-jupyter .highlight pre {
/* weird, but --jp-code-padding defined to be 5px but 4px horizontal padding is hardcoded for pre.cm-line */
  padding: var(--jp-code-padding) 4px;
  margin: 0;

  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  color: inherit;

}

.jp-OutputArea-output pre {
  line-height: inherit;
  font-family: inherit;
}

.jp-RenderedText pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
}

/* Hiding the collapser by default */
.jp-Collapser {
  display: none;
}

@page {
    margin: 0.5in; /* Margin for each printed piece of paper */
}

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}
</style>
<!-- Load mathjax -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-AMS_CHTML-full,Safe"> </script>
<!-- MathJax configuration -->
<script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                messageStyle: 'none',
                CommonHTML: {
                    linebreaks: {
                    automatic: true
                    }
                }
            });

            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
<!-- End of mathjax configuration --><script type="module">
  document.addEventListener("DOMContentLoaded", async () => {
    const diagrams = document.querySelectorAll(".jp-Mermaid > pre.mermaid");
    // do not load mermaidjs if not needed
    if (!diagrams.length) {
      return;
    }
    const mermaid = (await import("https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.7.0/mermaid.esm.min.mjs")).default;
    const parser = new DOMParser();

    mermaid.initialize({
      maxTextSize: 100000,
      maxEdges: 100000,
      startOnLoad: false,
      fontFamily: window
        .getComputedStyle(document.body)
        .getPropertyValue("--jp-ui-font-family"),
      theme: document.querySelector("body[data-jp-theme-light='true']")
        ? "default"
        : "dark",
    });

    let _nextMermaidId = 0;

    function makeMermaidImage(svg) {
      const img = document.createElement("img");
      const doc = parser.parseFromString(svg, "image/svg+xml");
      const svgEl = doc.querySelector("svg");
      const { maxWidth } = svgEl?.style || {};
      const firstTitle = doc.querySelector("title");
      const firstDesc = doc.querySelector("desc");

      img.setAttribute("src", `data:image/svg+xml,${encodeURIComponent(svg)}`);
      if (maxWidth) {
        img.width = parseInt(maxWidth);
      }
      if (firstTitle) {
        img.setAttribute("alt", firstTitle.textContent);
      }
      if (firstDesc) {
        const caption = document.createElement("figcaption");
        caption.className = "sr-only";
        caption.textContent = firstDesc.textContent;
        return [img, caption];
      }
      return [img];
    }

    async function makeMermaidError(text) {
      let errorMessage = "";
      try {
        await mermaid.parse(text);
      } catch (err) {
        errorMessage = `${err}`;
      }

      const result = document.createElement("details");
      result.className = 'jp-RenderedMermaid-Details';
      const summary = document.createElement("summary");
      summary.className = 'jp-RenderedMermaid-Summary';
      const pre = document.createElement("pre");
      const code = document.createElement("code");
      code.innerText = text;
      pre.appendChild(code);
      summary.appendChild(pre);
      result.appendChild(summary);

      const warning = document.createElement("pre");
      warning.innerText = errorMessage;
      result.appendChild(warning);
      return [result];
    }

    async function renderOneMarmaid(src) {
      const id = `jp-mermaid-${_nextMermaidId++}`;
      const parent = src.parentNode;
      let raw = src.textContent.trim();
      const el = document.createElement("div");
      el.style.visibility = "hidden";
      document.body.appendChild(el);
      let results = null;
      let output = null;
      try {
        let { svg } = await mermaid.render(id, raw, el);
        svg = cleanMermaidSvg(svg);
        results = makeMermaidImage(svg);
        output = document.createElement("figure");
        results.map(output.appendChild, output);
      } catch (err) {
        parent.classList.add("jp-mod-warning");
        results = await makeMermaidError(raw);
        output = results[0];
      } finally {
        el.remove();
      }
      parent.classList.add("jp-RenderedMermaid");
      parent.appendChild(output);
    }


    /**
     * Post-process to ensure mermaid diagrams contain only valid SVG and XHTML.
     */
    function cleanMermaidSvg(svg) {
      return svg.replace(RE_VOID_ELEMENT, replaceVoidElement);
    }


    /**
     * A regular expression for all void elements, which may include attributes and
     * a slash.
     *
     * @see https://developer.mozilla.org/en-US/docs/Glossary/Void_element
     *
     * Of these, only `<br>` is generated by Mermaid in place of `\n`,
     * but _any_ "malformed" tag will break the SVG rendering entirely.
     */
    const RE_VOID_ELEMENT =
      /<\s*(area|base|br|col|embed|hr|img|input|link|meta|param|source|track|wbr)\s*([^>]*?)\s*>/gi;

    /**
     * Ensure a void element is closed with a slash, preserving any attributes.
     */
    function replaceVoidElement(match, tag, rest) {
      rest = rest.trim();
      if (!rest.endsWith('/')) {
        rest = `${rest} /`;
      }
      return `<${tag} ${rest}>`;
    }

    void Promise.all([...diagrams].map(renderOneMarmaid));
  });
</script>
<style>
  .jp-Mermaid:not(.jp-RenderedMermaid) {
    display: none;
  }

  .jp-RenderedMermaid {
    overflow: auto;
    display: flex;
  }

  .jp-RenderedMermaid.jp-mod-warning {
    width: auto;
    padding: 0.5em;
    margin-top: 0.5em;
    border: var(--jp-border-width) solid var(--jp-warn-color2);
    border-radius: var(--jp-border-radius);
    color: var(--jp-ui-font-color1);
    font-size: var(--jp-ui-font-size1);
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  .jp-RenderedMermaid figure {
    margin: 0;
    overflow: auto;
    max-width: 100%;
  }

  .jp-RenderedMermaid img {
    max-width: 100%;
  }

  .jp-RenderedMermaid-Details > pre {
    margin-top: 1em;
  }

  .jp-RenderedMermaid-Summary {
    color: var(--jp-warn-color2);
  }

  .jp-RenderedMermaid:not(.jp-mod-warning) pre {
    display: none;
  }

  .jp-RenderedMermaid-Summary > pre {
    display: inline-block;
    white-space: normal;
  }
</style>
<!-- End of mermaid configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">
<main>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="Mileage-Prediction---Linear-Regression-Analysis"><strong>Mileage Prediction - Linear Regression Analysis</strong><a class="anchor-link" href="#Mileage-Prediction---Linear-Regression-Analysis">¶</a></h1>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<hr/>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Objective"><strong>Objective</strong><a class="anchor-link" href="#Objective">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>The objective of this project is to develop a predictive model that accurately estimates the fuel efficiency of vehicles, measured in miles per gallon (mpg) based on various vehicle attributes such as engine displacement, horsepower, weight, acceleration, and other relevant features.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Data-Source"><strong>Data Source</strong><a class="anchor-link" href="#Data-Source">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>This dataset was taken from the StatLib library which is maintained at Carnegie Mellon University, The dataset was used in the 1983 American Statistical Association Exposition. This dataset is a slightly modified version of the dataset provided in the StatLib library. In line with the use by Ross Quinlan (1993) in predicting the attribute <em>mpg</em>, 8 of the original instances were removed because they had unknown values for the "mpg" attribute.
"The data concerns city-cycle fuel consumption in miles per gallon, to be predicted in terms of 3 multivalued discrete and 5 continuous attributes" (Quinlan, 1993).</p>
<h1 id="Attribute-Information:"><strong>Attribute Information</strong>:<a class="anchor-link" href="#Attribute-Information:">¶</a></h1><ol>
<li>mpg: continuous</li>
<li>cylinders: multi-valued discrete</li>
<li>displacement: continuous</li>
<li>horsepower: continuous</li>
<li>weight: continuous</li>
<li>acceleration: continuous</li>
<li>model year: multi-valued discrete</li>
<li>origin: multi-valued discrete</li>
<li>car name: string (unique for each instance)</li>
</ol>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Import-Library"><strong>Import Library</strong><a class="anchor-link" href="#Import-Library">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [1]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span><span class="w"> </span><span class="nn">pandas</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">pd</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">numpy</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">np</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">matplotlib.pyplot</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">plt</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">seaborn</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">sns</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Import-Data"><strong>Import Data</strong><a class="anchor-link" href="#Import-Data">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [2]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'https://github.com/YBIFoundation/Dataset/blob/main/MPG.csv?raw=true'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [3]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[3]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>mpg</th>
<th>cylinders</th>
<th>displacement</th>
<th>horsepower</th>
<th>weight</th>
<th>acceleration</th>
<th>model_year</th>
<th>origin</th>
<th>name</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>18.0</td>
<td>8</td>
<td>307.0</td>
<td>130.0</td>
<td>3504</td>
<td>12.0</td>
<td>70</td>
<td>usa</td>
<td>chevrolet chevelle malibu</td>
</tr>
<tr>
<th>1</th>
<td>15.0</td>
<td>8</td>
<td>350.0</td>
<td>165.0</td>
<td>3693</td>
<td>11.5</td>
<td>70</td>
<td>usa</td>
<td>buick skylark 320</td>
</tr>
<tr>
<th>2</th>
<td>18.0</td>
<td>8</td>
<td>318.0</td>
<td>150.0</td>
<td>3436</td>
<td>11.0</td>
<td>70</td>
<td>usa</td>
<td>plymouth satellite</td>
</tr>
<tr>
<th>3</th>
<td>16.0</td>
<td>8</td>
<td>304.0</td>
<td>150.0</td>
<td>3433</td>
<td>12.0</td>
<td>70</td>
<td>usa</td>
<td>amc rebel sst</td>
</tr>
<tr>
<th>4</th>
<td>17.0</td>
<td>8</td>
<td>302.0</td>
<td>140.0</td>
<td>3449</td>
<td>10.5</td>
<td>70</td>
<td>usa</td>
<td>ford torino</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [4]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">nunique</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[4]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>mpg             129
cylinders         5
displacement     82
horsepower       93
weight          351
acceleration     95
model_year       13
origin            3
name            305
dtype: int64</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Describe-Data"><strong>Describe Data</strong><a class="anchor-link" href="#Describe-Data">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [5]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 398 entries, 0 to 397
Data columns (total 9 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   mpg           398 non-null    float64
 1   cylinders     398 non-null    int64  
 2   displacement  398 non-null    float64
 3   horsepower    392 non-null    float64
 4   weight        398 non-null    int64  
 5   acceleration  398 non-null    float64
 6   model_year    398 non-null    int64  
 7   origin        398 non-null    object 
 8   name          398 non-null    object 
dtypes: float64(4), int64(3), object(2)
memory usage: 28.1+ KB
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [6]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[6]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>mpg</th>
<th>cylinders</th>
<th>displacement</th>
<th>horsepower</th>
<th>weight</th>
<th>acceleration</th>
<th>model_year</th>
</tr>
</thead>
<tbody>
<tr>
<th>count</th>
<td>398.000000</td>
<td>398.000000</td>
<td>398.000000</td>
<td>392.000000</td>
<td>398.000000</td>
<td>398.000000</td>
<td>398.000000</td>
</tr>
<tr>
<th>mean</th>
<td>23.514573</td>
<td>5.454774</td>
<td>193.425879</td>
<td>104.469388</td>
<td>2970.424623</td>
<td>15.568090</td>
<td>76.010050</td>
</tr>
<tr>
<th>std</th>
<td>7.815984</td>
<td>1.701004</td>
<td>104.269838</td>
<td>38.491160</td>
<td>846.841774</td>
<td>2.757689</td>
<td>3.697627</td>
</tr>
<tr>
<th>min</th>
<td>9.000000</td>
<td>3.000000</td>
<td>68.000000</td>
<td>46.000000</td>
<td>1613.000000</td>
<td>8.000000</td>
<td>70.000000</td>
</tr>
<tr>
<th>25%</th>
<td>17.500000</td>
<td>4.000000</td>
<td>104.250000</td>
<td>75.000000</td>
<td>2223.750000</td>
<td>13.825000</td>
<td>73.000000</td>
</tr>
<tr>
<th>50%</th>
<td>23.000000</td>
<td>4.000000</td>
<td>148.500000</td>
<td>93.500000</td>
<td>2803.500000</td>
<td>15.500000</td>
<td>76.000000</td>
</tr>
<tr>
<th>75%</th>
<td>29.000000</td>
<td>8.000000</td>
<td>262.000000</td>
<td>126.000000</td>
<td>3608.000000</td>
<td>17.175000</td>
<td>79.000000</td>
</tr>
<tr>
<th>max</th>
<td>46.600000</td>
<td>8.000000</td>
<td>455.000000</td>
<td>230.000000</td>
<td>5140.000000</td>
<td>24.800000</td>
<td>82.000000</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Data-Visualization"><strong>Data Visualization</strong><a class="anchor-link" href="#Data-Visualization">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [7]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">sns</span><span class="o">.</span><span class="n">pairplot</span><span class="p">(</span><span class="n">df</span><span class="p">,</span> <span class="n">x_vars</span><span class="o">=</span><span class="p">[</span><span class="s1">'displacement'</span><span class="p">,</span> <span class="s1">'horsepower'</span><span class="p">,</span> <span class="s1">'weight'</span><span class="p">,</span> <span class="s1">'acceleration'</span><span class="p">,</span> <span class="s1">'mpg'</span><span class="p">],</span> <span class="n">y_vars</span><span class="o">=</span><span class="p">[</span><span class="s1">'mpg'</span><span class="p">])</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[7]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>&lt;seaborn.axisgrid.PairGrid at 0x213f7410ad0&gt;</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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"/>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [8]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">sns</span><span class="o">.</span><span class="n">regplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">'displacement'</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">'mpg'</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">df</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[8]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>&lt;Axes: xlabel='displacement', ylabel='mpg'&gt;</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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7faQ28O6Z511VsCy733ve56zzz7b/xi/glatWhV2nx544AHPMccc4398/PHHey677LKQ6x48eNCj0+k8VVVVAcsXL17sWbZsGf+8YsUKfs+ysjL/89dee60nLS2Nj1/hzDPP5OUD2e5DDz3kKSws9D9eunSp5/zzzw97rIIg9A+pkREEgSkvLye73c5pE4W8vDxOwYQCUQmkmZACQqQBUZLzzjuP9PruXyvHH398wGvwuLeup//85z8cLcG+tLe3k9PppKysLP/zW7dupauvvjrka7dv387pIKSm1CAtlJ+f73+MdNLEiRP9jwsLCzmlhHSQelldXd2AtovUnLINQRAGDxEygiD0i9LSUtq9eze9//77nC664YYbOJWE1JTBYOjz9pC6ueyyy+jee++lM888k7KzszmVo67TsVgsYV8P4aPT6WjTpk18r0YtUoL3DfUqoZa53e4Bb9cbdBIEYTARISMIAoNoAi7G69ev5wJe0NTURHv27KFTTz015GsgLBCFwe3GG2+kadOmcQRj3rx5/Py6desC1sdjFMOG4rPPPqOxY8fSL37xC/+ygwcPBqwzZ84crou58sore7z+6KOP5sgJoiAnn3wyxYpYbddoNAYUEAuCEBtEyAiC4I8uXHXVVVzwi5TJyJEjWVRotaF7AlCUiwszUlFIq/z73/9mYQMxovDpp5/SH/7wB7rgggs4avPiiy9ywW4oJk+ezAWyiMKgKwnrrVq1KmCdX//617R48WIWXZdccgmnnlCgq3Q7IaKDritEcSBA6uvrWfhAAJ177rn9+lxitV2kr9DVhCgWPl9EnPoTuRIEIRDpWhIEwQ9SQ4g6IMKyZMkSOumkk+iYY44JuS7ajdFVdOKJJ/IFHSkmtEar60Zuv/122rhxI1/877vvPvrzn//MaaNQfOtb36Jbb72VO4SOOuoojtCg/TrYZRhi6L///S+vc/rpp9OGDRv8z69YsYIFB94XtT0QUDDxUyJM/SUW20VtD147f/589uOByBMEYeBoUPEbg+0IgiD0iEBgtIEy3kAQBGEwkIiMIAiCIAhJiwgZQRAEQRCSFkktCYIgCIKQtEhERhAEQRCEpEWEjCAIgiAISYsIGUEQBEEQkhYRMoIgCIIgJC0iZARBEARBSFpEyAiCIAiCkLSIkBEEQRAEIWkRISMIgiAIAiUr/x8yjRTZ7VtWNAAAAABJRU5ErkJggg=="/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Data-Preprocessing"><strong>Data Preprocessing</strong><a class="anchor-link" href="#Data-Preprocessing">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [9]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">dropna</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [10]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
Index: 392 entries, 0 to 397
Data columns (total 9 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   mpg           392 non-null    float64
 1   cylinders     392 non-null    int64  
 2   displacement  392 non-null    float64
 3   horsepower    392 non-null    float64
 4   weight        392 non-null    int64  
 5   acceleration  392 non-null    float64
 6   model_year    392 non-null    int64  
 7   origin        392 non-null    object 
 8   name          392 non-null    object 
dtypes: float64(4), int64(3), object(2)
memory usage: 30.6+ KB
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Define-Target-Variable-(y)-and-Feature-Variables-(X)"><strong>Define Target Variable (y) and Feature Variables (X)</strong><a class="anchor-link" href="#Define-Target-Variable-(y)-and-Feature-Variables-(X)">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [11]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">columns</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[11]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>Index(['mpg', 'cylinders', 'displacement', 'horsepower', 'weight',
       'acceleration', 'model_year', 'origin', 'name'],
      dtype='object')</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [12]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">y</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s1">'mpg'</span><span class="p">]</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [13]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">y</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[13]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(392,)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [14]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s1">'displacement'</span><span class="p">,</span> <span class="s1">'horsepower'</span><span class="p">,</span> <span class="s1">'weight'</span><span class="p">,</span> <span class="s1">'acceleration'</span><span class="p">]]</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [15]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[15]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(392, 4)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [16]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[16]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>displacement</th>
<th>horsepower</th>
<th>weight</th>
<th>acceleration</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>307.0</td>
<td>130.0</td>
<td>3504</td>
<td>12.0</td>
</tr>
<tr>
<th>1</th>
<td>350.0</td>
<td>165.0</td>
<td>3693</td>
<td>11.5</td>
</tr>
<tr>
<th>2</th>
<td>318.0</td>
<td>150.0</td>
<td>3436</td>
<td>11.0</td>
</tr>
<tr>
<th>3</th>
<td>304.0</td>
<td>150.0</td>
<td>3433</td>
<td>12.0</td>
</tr>
<tr>
<th>4</th>
<td>302.0</td>
<td>140.0</td>
<td>3449</td>
<td>10.5</td>
</tr>
<tr>
<th>...</th>
<td>...</td>
<td>...</td>
<td>...</td>
<td>...</td>
</tr>
<tr>
<th>393</th>
<td>140.0</td>
<td>86.0</td>
<td>2790</td>
<td>15.6</td>
</tr>
<tr>
<th>394</th>
<td>97.0</td>
<td>52.0</td>
<td>2130</td>
<td>24.6</td>
</tr>
<tr>
<th>395</th>
<td>135.0</td>
<td>84.0</td>
<td>2295</td>
<td>11.6</td>
</tr>
<tr>
<th>396</th>
<td>120.0</td>
<td>79.0</td>
<td>2625</td>
<td>18.6</td>
</tr>
<tr>
<th>397</th>
<td>119.0</td>
<td>82.0</td>
<td>2720</td>
<td>19.4</td>
</tr>
</tbody>
</table>
<p>392 rows × 4 columns</p>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Data-Scalling">Data Scalling<a class="anchor-link" href="#Data-Scalling">¶</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [17]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span><span class="w"> </span><span class="nn">sklearn.preprocessing</span><span class="w"> </span><span class="kn">import</span> <span class="n">StandardScaler</span>
<span class="n">ss</span> <span class="o">=</span> <span class="n">StandardScaler</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [18]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x</span> <span class="o">=</span> <span class="n">ss</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [19]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[19]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>array([[ 1.07728956,  0.66413273,  0.62054034, -1.285258  ],
       [ 1.48873169,  1.57459447,  0.84333403, -1.46672362],
       [ 1.1825422 ,  1.18439658,  0.54038176, -1.64818924],
       ...,
       [-0.56847897, -0.53247413, -0.80463202, -1.4304305 ],
       [-0.7120053 , -0.66254009, -0.41562716,  1.11008813],
       [-0.72157372, -0.58450051, -0.30364091,  1.40043312]],
      shape=(392, 4))</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [20]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">x</span><span class="p">)</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[20]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>0</th>
<th>1</th>
<th>2</th>
<th>3</th>
</tr>
</thead>
<tbody>
<tr>
<th>count</th>
<td>3.920000e+02</td>
<td>3.920000e+02</td>
<td>3.920000e+02</td>
<td>3.920000e+02</td>
</tr>
<tr>
<th>mean</th>
<td>-7.250436e-17</td>
<td>-1.812609e-16</td>
<td>-1.812609e-17</td>
<td>4.350262e-16</td>
</tr>
<tr>
<th>std</th>
<td>1.001278e+00</td>
<td>1.001278e+00</td>
<td>1.001278e+00</td>
<td>1.001278e+00</td>
</tr>
<tr>
<th>min</th>
<td>-1.209563e+00</td>
<td>-1.520975e+00</td>
<td>-1.608575e+00</td>
<td>-2.736983e+00</td>
</tr>
<tr>
<th>25%</th>
<td>-8.555316e-01</td>
<td>-7.665929e-01</td>
<td>-8.868535e-01</td>
<td>-6.410551e-01</td>
</tr>
<tr>
<th>50%</th>
<td>-4.153842e-01</td>
<td>-2.853488e-01</td>
<td>-2.052109e-01</td>
<td>-1.499869e-02</td>
</tr>
<tr>
<th>75%</th>
<td>7.782764e-01</td>
<td>5.600800e-01</td>
<td>7.510927e-01</td>
<td>5.384714e-01</td>
</tr>
<tr>
<th>max</th>
<td>2.493416e+00</td>
<td>3.265452e+00</td>
<td>2.549061e+00</td>
<td>3.360262e+00</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Train-Test-Split"><strong>Train Test Split</strong><a class="anchor-link" href="#Train-Test-Split">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [21]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span><span class="w"> </span><span class="nn">sklearn.model_selection</span><span class="w"> </span><span class="kn">import</span> <span class="n">train_test_split</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [22]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x_train</span><span class="p">,</span> <span class="n">x_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span><span class="o">=</span><span class="mf">0.7</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">2529</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [23]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">x_train</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">x_test</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">y_train</span><span class="o">.</span><span class="n">shape</span><span class="p">,</span> <span class="n">y_test</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[23]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>((117, 4), (275, 4), (117,), (275,))</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Modeling"><strong>Modeling</strong><a class="anchor-link" href="#Modeling">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [24]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span><span class="w"> </span><span class="nn">sklearn.linear_model</span><span class="w"> </span><span class="kn">import</span> <span class="n">LinearRegression</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">LinearRegression</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [25]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">x_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[25]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<style>#sk-container-id-1 {
  /* Definition of color scheme common for light and dark mode */
  --sklearn-color-text: #000;
  --sklearn-color-text-muted: #666;
  --sklearn-color-line: gray;
  /* Definition of color scheme for unfitted estimators */
  --sklearn-color-unfitted-level-0: #fff5e6;
  --sklearn-color-unfitted-level-1: #f6e4d2;
  --sklearn-color-unfitted-level-2: #ffe0b3;
  --sklearn-color-unfitted-level-3: chocolate;
  /* Definition of color scheme for fitted estimators */
  --sklearn-color-fitted-level-0: #f0f8ff;
  --sklearn-color-fitted-level-1: #d4ebff;
  --sklearn-color-fitted-level-2: #b3dbfd;
  --sklearn-color-fitted-level-3: cornflowerblue;

  /* Specific color for light theme */
  --sklearn-color-text-on-default-background: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, black)));
  --sklearn-color-background: var(--sg-background-color, var(--theme-background, var(--jp-layout-color0, white)));
  --sklearn-color-border-box: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, black)));
  --sklearn-color-icon: #696969;

  @media (prefers-color-scheme: dark) {
    /* Redefinition of color scheme for dark theme */
    --sklearn-color-text-on-default-background: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, white)));
    --sklearn-color-background: var(--sg-background-color, var(--theme-background, var(--jp-layout-color0, #111)));
    --sklearn-color-border-box: var(--sg-text-color, var(--theme-code-foreground, var(--jp-content-font-color1, white)));
    --sklearn-color-icon: #878787;
  }
}

#sk-container-id-1 {
  color: var(--sklearn-color-text);
}

#sk-container-id-1 pre {
  padding: 0;
}

#sk-container-id-1 input.sk-hidden--visually {
  border: 0;
  clip: rect(1px 1px 1px 1px);
  clip: rect(1px, 1px, 1px, 1px);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
}

#sk-container-id-1 div.sk-dashed-wrapped {
  border: 1px dashed var(--sklearn-color-line);
  margin: 0 0.4em 0.5em 0.4em;
  box-sizing: border-box;
  padding-bottom: 0.4em;
  background-color: var(--sklearn-color-background);
}

#sk-container-id-1 div.sk-container {
  /* jupyter's `normalize.less` sets `[hidden] { display: none; }`
     but bootstrap.min.css set `[hidden] { display: none !important; }`
     so we also need the `!important` here to be able to override the
     default hidden behavior on the sphinx rendered scikit-learn.org.
     See: https://github.com/scikit-learn/scikit-learn/issues/21755 */
  display: inline-block !important;
  position: relative;
}

#sk-container-id-1 div.sk-text-repr-fallback {
  display: none;
}

div.sk-parallel-item,
div.sk-serial,
div.sk-item {
  /* draw centered vertical line to link estimators */
  background-image: linear-gradient(var(--sklearn-color-text-on-default-background), var(--sklearn-color-text-on-default-background));
  background-size: 2px 100%;
  background-repeat: no-repeat;
  background-position: center center;
}

/* Parallel-specific style estimator block */

#sk-container-id-1 div.sk-parallel-item::after {
  content: "";
  width: 100%;
  border-bottom: 2px solid var(--sklearn-color-text-on-default-background);
  flex-grow: 1;
}

#sk-container-id-1 div.sk-parallel {
  display: flex;
  align-items: stretch;
  justify-content: center;
  background-color: var(--sklearn-color-background);
  position: relative;
}

#sk-container-id-1 div.sk-parallel-item {
  display: flex;
  flex-direction: column;
}

#sk-container-id-1 div.sk-parallel-item:first-child::after {
  align-self: flex-end;
  width: 50%;
}

#sk-container-id-1 div.sk-parallel-item:last-child::after {
  align-self: flex-start;
  width: 50%;
}

#sk-container-id-1 div.sk-parallel-item:only-child::after {
  width: 0;
}

/* Serial-specific style estimator block */

#sk-container-id-1 div.sk-serial {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: var(--sklearn-color-background);
  padding-right: 1em;
  padding-left: 1em;
}


/* Toggleable style: style used for estimator/Pipeline/ColumnTransformer box that is
clickable and can be expanded/collapsed.
- Pipeline and ColumnTransformer use this feature and define the default style
- Estimators will overwrite some part of the style using the `sk-estimator` class
*/

/* Pipeline and ColumnTransformer style (default) */

#sk-container-id-1 div.sk-toggleable {
  /* Default theme specific background. It is overwritten whether we have a
  specific estimator or a Pipeline/ColumnTransformer */
  background-color: var(--sklearn-color-background);
}

/* Toggleable label */
#sk-container-id-1 label.sk-toggleable__label {
  cursor: pointer;
  display: flex;
  width: 100%;
  margin-bottom: 0;
  padding: 0.5em;
  box-sizing: border-box;
  text-align: center;
  align-items: start;
  justify-content: space-between;
  gap: 0.5em;
}

#sk-container-id-1 label.sk-toggleable__label .caption {
  font-size: 0.6rem;
  font-weight: lighter;
  color: var(--sklearn-color-text-muted);
}

#sk-container-id-1 label.sk-toggleable__label-arrow:before {
  /* Arrow on the left of the label */
  content: "▸";
  float: left;
  margin-right: 0.25em;
  color: var(--sklearn-color-icon);
}

#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {
  color: var(--sklearn-color-text);
}

/* Toggleable content - dropdown */

#sk-container-id-1 div.sk-toggleable__content {
  max-height: 0;
  max-width: 0;
  overflow: hidden;
  text-align: left;
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content.fitted {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content pre {
  margin: 0.2em;
  border-radius: 0.25em;
  color: var(--sklearn-color-text);
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-toggleable__content.fitted pre {
  /* unfitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {
  /* Expand drop-down */
  max-height: 200px;
  max-width: 100%;
  overflow: auto;
}

#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {
  content: "▾";
}

/* Pipeline/ColumnTransformer-specific style */

#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-label.fitted input.sk-toggleable__control:checked~label.sk-toggleable__label {
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Estimator-specific style */

/* Colorize estimator box */
#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-estimator.fitted input.sk-toggleable__control:checked~label.sk-toggleable__label {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-2);
}

#sk-container-id-1 div.sk-label label.sk-toggleable__label,
#sk-container-id-1 div.sk-label label {
  /* The background is the default theme color */
  color: var(--sklearn-color-text-on-default-background);
}

/* On hover, darken the color of the background */
#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-unfitted-level-2);
}

/* Label box, darken color on hover, fitted */
#sk-container-id-1 div.sk-label.fitted:hover label.sk-toggleable__label.fitted {
  color: var(--sklearn-color-text);
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Estimator label */

#sk-container-id-1 div.sk-label label {
  font-family: monospace;
  font-weight: bold;
  display: inline-block;
  line-height: 1.2em;
}

#sk-container-id-1 div.sk-label-container {
  text-align: center;
}

/* Estimator-specific */
#sk-container-id-1 div.sk-estimator {
  font-family: monospace;
  border: 1px dotted var(--sklearn-color-border-box);
  border-radius: 0.25em;
  box-sizing: border-box;
  margin-bottom: 0.5em;
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-0);
}

#sk-container-id-1 div.sk-estimator.fitted {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-0);
}

/* on hover */
#sk-container-id-1 div.sk-estimator:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-2);
}

#sk-container-id-1 div.sk-estimator.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-2);
}

/* Specification for estimator info (e.g. "i" and "?") */

/* Common style for "i" and "?" */

.sk-estimator-doc-link,
a:link.sk-estimator-doc-link,
a:visited.sk-estimator-doc-link {
  float: right;
  font-size: smaller;
  line-height: 1em;
  font-family: monospace;
  background-color: var(--sklearn-color-background);
  border-radius: 1em;
  height: 1em;
  width: 1em;
  text-decoration: none !important;
  margin-left: 0.5em;
  text-align: center;
  /* unfitted */
  border: var(--sklearn-color-unfitted-level-1) 1pt solid;
  color: var(--sklearn-color-unfitted-level-1);
}

.sk-estimator-doc-link.fitted,
a:link.sk-estimator-doc-link.fitted,
a:visited.sk-estimator-doc-link.fitted {
  /* fitted */
  border: var(--sklearn-color-fitted-level-1) 1pt solid;
  color: var(--sklearn-color-fitted-level-1);
}

/* On hover */
div.sk-estimator:hover .sk-estimator-doc-link:hover,
.sk-estimator-doc-link:hover,
div.sk-label-container:hover .sk-estimator-doc-link:hover,
.sk-estimator-doc-link:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

div.sk-estimator.fitted:hover .sk-estimator-doc-link.fitted:hover,
.sk-estimator-doc-link.fitted:hover,
div.sk-label-container:hover .sk-estimator-doc-link.fitted:hover,
.sk-estimator-doc-link.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

/* Span, style for the box shown on hovering the info icon */
.sk-estimator-doc-link span {
  display: none;
  z-index: 9999;
  position: relative;
  font-weight: normal;
  right: .2ex;
  padding: .5ex;
  margin: .5ex;
  width: min-content;
  min-width: 20ex;
  max-width: 50ex;
  color: var(--sklearn-color-text);
  box-shadow: 2pt 2pt 4pt #999;
  /* unfitted */
  background: var(--sklearn-color-unfitted-level-0);
  border: .5pt solid var(--sklearn-color-unfitted-level-3);
}

.sk-estimator-doc-link.fitted span {
  /* fitted */
  background: var(--sklearn-color-fitted-level-0);
  border: var(--sklearn-color-fitted-level-3);
}

.sk-estimator-doc-link:hover span {
  display: block;
}

/* "?"-specific style due to the `<a>` HTML tag */

#sk-container-id-1 a.estimator_doc_link {
  float: right;
  font-size: 1rem;
  line-height: 1em;
  font-family: monospace;
  background-color: var(--sklearn-color-background);
  border-radius: 1rem;
  height: 1rem;
  width: 1rem;
  text-decoration: none;
  /* unfitted */
  color: var(--sklearn-color-unfitted-level-1);
  border: var(--sklearn-color-unfitted-level-1) 1pt solid;
}

#sk-container-id-1 a.estimator_doc_link.fitted {
  /* fitted */
  border: var(--sklearn-color-fitted-level-1) 1pt solid;
  color: var(--sklearn-color-fitted-level-1);
}

/* On hover */
#sk-container-id-1 a.estimator_doc_link:hover {
  /* unfitted */
  background-color: var(--sklearn-color-unfitted-level-3);
  color: var(--sklearn-color-background);
  text-decoration: none;
}

#sk-container-id-1 a.estimator_doc_link.fitted:hover {
  /* fitted */
  background-color: var(--sklearn-color-fitted-level-3);
}
</style><div class="sk-top-container" id="sk-container-id-1"><div class="sk-text-repr-fallback"><pre>LinearRegression()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br/>On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden=""><div class="sk-item"><div class="sk-estimator fitted sk-toggleable"><input checked="" class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox"/><label class="sk-toggleable__label fitted sk-toggleable__label-arrow" for="sk-estimator-id-1"><div><div>LinearRegression</div></div><div><a class="sk-estimator-doc-link fitted" href="https://scikit-learn.org/1.6/modules/generated/sklearn.linear_model.LinearRegression.html" rel="noreferrer" target="_blank">?<span>Documentation for LinearRegression</span></a><span class="sk-estimator-doc-link fitted">i<span>Fitted</span></span></div></label><div class="sk-toggleable__content fitted"><pre>LinearRegression()</pre></div> </div></div></div></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [26]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">model</span><span class="o">.</span><span class="n">intercept_</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[26]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>np.float64(23.601118059983822)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [27]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">model</span><span class="o">.</span><span class="n">coef_</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[27]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>array([-1.07085922, -0.64133484, -5.18021642,  0.26756035])</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Mileage = 23.60 - 1.07 x Displacement - 0.54 x horsepower - 5.18 x weight - 0.26 x accelaration + error</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Prediction"><strong>Prediction</strong><a class="anchor-link" href="#Prediction">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [28]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">y_pred</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">x_test</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [29]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">y_pred</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[29]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>array([18.83232615, 14.67689764, 13.90916105, 23.48706843, 30.25543552,
       23.46671071, 27.28163576, 24.60121655, 14.40764431, 10.81692289,
       24.30874146, 27.9134718 , 31.87135668, 31.42289874, 17.69562279,
       19.09989244, 28.60563403, 32.67685665, 31.45063299, 27.35959705,
       18.46314382, 22.19920123, 26.2982957 , 33.03335117, 20.48801313,
        9.54351607, 22.40016431, 18.3349025 , 24.90567933, 17.72005616,
       23.00135022, 16.88953804, 10.57530881, 30.26775706, 20.13255834,
       29.29639211, 24.89285218, 21.37238187,  9.68643504, 12.73666785,
       20.95618571, 20.11237202,  6.42862798, 17.31748152, 22.17367358,
       29.47288305, 13.72946495, 25.84603835, 30.3260242 , 22.49617884,
       21.32125793, 16.21218023, 23.82532354, 30.39683971,  9.25868474,
       10.87274956, 28.51433586, 23.14656115, 20.00708585, 31.00621369,
       20.4572209 , 27.13086597, 22.2195037 , 13.80505274, 25.30799492,
       27.41913866, 15.02111221, 24.0510285 , 31.58339665, 14.71198437,
       28.40951415, 24.38955292, 10.32744169, 30.34649857, 31.36890215,
       27.54419109, 31.45951656, 11.79997332, 27.91621479, 16.39826116,
       26.00741208, 29.91277112, 14.38156189, 34.01866663, 31.13639458,
       31.62182158, 14.30925712, 27.2926804 , 26.63435828, 29.37881754,
       32.99444728, 29.6050515 , 32.10514989, 32.25284797, 21.13168172,
       33.0252248 , 26.90038554, 29.52975708, 31.75501067, 24.98501933,
       18.5377402 , 23.47017909, 23.42300088, 21.78885537, 16.23596383,
       29.33381668, 26.05070165, 12.26181347, 26.05586523, 31.22476543,
       21.24570017, 14.91388264, 31.03381591, 29.12769038, 29.66701721,
       29.70042089, 20.83158998, 28.86124453,  9.91195685, 31.46954118,
       20.36121751, 16.56294385, 23.95954576, 16.46259556, 29.71022071,
        8.25384047, 17.98858966, 28.25327318, 28.55437284, 33.21571931,
       28.93271325, 24.95943138, 25.11347485, 15.36443891, 29.70469252,
       18.34172812, 32.66023428, 10.63443799, 16.11425046, 29.62906892,
       27.23175923, 30.44542586, 29.93026938, 20.76067501, 26.78107967,
       12.659952  , 13.92484922,  7.18792728, 30.63795392, 23.86752328,
       31.01633435, 29.17774074, 24.22235964, 11.37969831, 31.51747369,
       30.54109825, 21.96045234, 10.95206506, 24.55911365, 31.37485518,
       28.05996384, 31.41656139, 32.37966212, 32.98793573, 29.89694289,
       12.86362348, 26.30056161, 30.54723934, 23.9706354 , 31.47005419,
       31.52998327,  6.76932656, 29.02090816, 23.8793263 , 25.56920453,
       14.33987609, 29.03176984, 27.49133392, 29.55419223, 28.26259187,
       30.34415155,  8.38025482, 27.93261652, 18.63098325, 32.31082061,
       27.98085215, 20.57672078, 25.57013199, 32.92127709, 28.23868498,
       24.62655056, 29.07735332, 31.09386418, 28.75672725, 22.75423869,
       26.21011949, 25.81603414, 31.34989502, 25.85156184, 28.61800152,
       29.80352024, 16.58705288, 20.16881507, 30.89733167, 19.58793749,
       27.70529135, 19.15419098, 29.21391604, 21.19463598, 11.51525917,
       13.13358727, 26.72601846, 14.65194599, 18.59856609,  8.06814991,
       29.71476222, 12.18972081, 11.85436831, 31.20794967, 17.08578273,
       30.3135862 , 31.87760822, 23.41685328, 24.21621141, 32.2033722 ,
       14.07222319, 25.3192112 ,  9.97363047, 27.03125036, 27.93707144,
       23.53405231, 31.30735985, 30.19733987, 32.93098769, 21.05909955,
       26.797812  , 31.66162391, 16.67826212, 28.01477919, 31.60028449,
       14.15899628, 11.81125104, 31.96165945,  8.920501  , 28.33681473,
       22.70635452, 29.47573419, 19.71041699, 13.78350495, 15.98591599,
       26.25191436, 26.81371883, 24.57480539, 21.32843278, 25.14184107,
       31.48453559, 25.80104374, 25.99261035, 25.13901481, 21.40385185,
       27.23853972, 25.13754806, 25.03078556, 19.45970198, 30.9358871 ,
       23.72335234, 31.08062611, 15.1364889 , 17.76984239, 11.16102151,
       28.25581388, 27.4518097 , 28.45634197, 30.07250104, 20.46705742])</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Model-Evaluation"><strong>Model Evaluation</strong><a class="anchor-link" href="#Model-Evaluation">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [30]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">from</span><span class="w"> </span><span class="nn">sklearn.metrics</span><span class="w"> </span><span class="kn">import</span> <span class="n">mean_squared_error</span><span class="p">,</span> <span class="n">mean_absolute_error</span><span class="p">,</span> <span class="n">r2_score</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [31]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">mean_absolute_error</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[31]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>3.3564087099398776</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [32]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">mean_absolute_percentage_error</span> <span class="o">=</span> <span class="n">mean_absolute_error</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span> <span class="o">/</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">y_test</span><span class="p">)</span> <span class="o">*</span> <span class="mi">100</span>
<span class="n">mean_absolute_percentage_error</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[32]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>np.float64(14.280601467238085)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [33]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">mean_squared_error</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[33]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>18.66906130306789</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [34]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">r2_score</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[34]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>0.6923289624942408</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Mileage = 23.60 - 1.07 x Displacement - 0.54 x horsepower - 5.18 x weight - 0.26 x accelaration + error(3.35)</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Explaination"><strong>Explaination</strong><a class="anchor-link" href="#Explaination">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>The project aims to develop a predictive model to estimate the fuel efficiency of vehicles, measured in miles per gallon (mpg), based on various vehicle attributes. The dataset used contains information about vehicle specifications such as engine displacement, horsepower, weight, acceleration, and other features.</p>
<h3 id="Key-Steps:">Key Steps:<a class="anchor-link" href="#Key-Steps:">¶</a></h3><ol>
<li><strong>Data Exploration</strong>: The dataset was explored to understand its structure, data types, and unique values. Missing values were handled by dropping rows with null entries.</li>
<li><strong>Feature Selection</strong>: Relevant features such as displacement, horsepower, weight, and acceleration were selected as predictors, while mpg was chosen as the target variable.</li>
<li><strong>Data Scaling</strong>: The features were scaled using <code>StandardScaler</code> to normalize the data for better performance in regression modeling.</li>
<li><strong>Train-Test Split</strong>: The dataset was split into training and testing sets with a 70-30 ratio to evaluate the model's performance.</li>
<li><strong>Modeling</strong>: A linear regression model was trained on the training data to predict mpg based on the selected features.</li>
<li><strong>Evaluation</strong>: The model's performance was evaluated using metrics such as Mean Absolute Error (MAE), Mean Squared Error (MSE), and R-squared (R²). The model achieved a reasonable level of accuracy in predicting mpg.</li>
</ol>
<h3 id="Conclusion:">Conclusion:<a class="anchor-link" href="#Conclusion:">¶</a></h3><p>The linear regression model provides a mathematical equation to predict mpg based on vehicle attributes. The model's coefficients indicate the impact of each feature on mpg. For example, an increase in weight negatively impacts mpg, as shown by the negative coefficient for weight. The model can be further improved by exploring additional features, handling multicollinearity, or using advanced regression techniques.</p>
</div>
</div>
</div>
</div>
</main>
</body>
</html>
