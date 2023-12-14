---
sidebar_position: 3
---

# React UI

ShrouvEngine uses [React Lua](https://github.com/jsdotlua/react-lua) to handle UI interaction which enables tons of really cool features

Default UI folder structure:

- `client/ui/context` - Custom React Contexts
- `client/ui/hooks` - Custom React Hooks
- `client/ui/library` - Custom UI Library Primitives
- `client/ui/modals` - Custom UI Modals
- `client/ui/stories` - UI Stories (Uses [Flipbook](https://github.com/flipbook-labs/flipbook))

Default UI folder files:

- `client/ui/app.tsx` - Main app file, contains all providers and uses overlay as child
- `client/ui/overlay.tsx` - Main overlay GUI, houses ModalProvider and HUD
- `client/ui/hud.tsx` - Main visible HUD

# UI Primitives

ShrouvEngine provides some mostly-unstyled example primitive components, [available here](https://github.com/mandrillxx/shrouvengine/tree/main/src/client/ui/library/index.tsx)

```typescript title="BaseProps"
export type BaseProps<T extends GuiObject> = Partial<{
  [K in keyof WritableInstanceProperties<T>]:
    | WritableInstanceProperties<T>[K]
    | Roact.Binding<WritableInstanceProperties<T>[K]>;
}> & {
  [key: string]: unknown;
  ref?: RefPropertyOrFunction<T>;
};
```

```typescript title="MouseEvent"
type MouseEvent = {
  MouseEnter?: () => void;
  MouseLeave?: () => void;
};
```

The following components are available:

```typescript title="Frame"
type IFrame = Roact.PropsWithChildren<BaseProps<Frame> & MouseEvent>;

export function Frame({
  Position,
  Size,
  Visible,
  BackgroundTransparency,
  BackgroundColor3,
  MouseEnter,
  MouseLeave,
  children,
}: IFrame);
```

```typescript title="Container"
type IContainer = Roact.PropsWithChildren<BaseProps<Frame>> & {
  AspectRatio?: number;
};

export function Container({
  Name,
  Position,
  Size,
  BackgroundTransparency,
  AspectRatio: IAspectRatio,
  children,
}: IContainer);
```

```typescript title="Canvas"
type ICanvas = Roact.PropsWithChildren<
  BaseProps<Frame> & { AspectRatio: number }
>;

export function Canvas({ AspectRatio, Visible, children }: ICanvas);
```

```typescript title="ImageButton"
type IImageButton = Roact.PropsWithChildren<BaseProps<ImageButton>> & {
  AspectRatio: number;
  Clicked?: () => void;
} & MouseEvent;

export function ImageButton({
  Name,
  Position,
  Size,
  Image,
  ImageColor3,
  BackgroundTransparency,
  Clicked,
  children,
  AspectRatio: IAspectRatio,
  MouseEnter,
  MouseLeave,
}: IImageButton);
```

```typescript title="ImageLabel"
type IImageLabel = Roact.PropsWithChildren<BaseProps<ImageLabel>> & {
  AspectRatio?: number;
};

export function ImageLabel({
  Position,
  Size,
  Image,
  ImageColor3,
  AspectRatio: IAspectRatio,
  children,
}: IImageLabel);
```

```typescript title="AspectRatio"
type IAspectRatio = Roact.PropsWithChildren<
  Partial<WritableInstanceProperties<UIAspectRatioConstraint>>
>;

export function AspectRatio({ AspectRatio }: IAspectRatio);
```

```typescript title="Gradient"
type IGradient = Partial<WritableInstanceProperties<UIGradient>>;

export function Gradient({ Color, Rotation, Transparency }: IGradient);
```

```typescript title="Text"
type IText = BaseProps<TextLabel> & { Thickness?: number };

export function Text({
  Text,
  Position,
  Size,
  RichText,
  TextColor3,
  Thickness,
}: IText);
```

```typescript title="Stroke"
type IStroke = Partial<WritableInstanceProperties<UIStroke>>;

export function Stroke({ Thickness }: IStroke);
```

```typescript title="Padding"
type IPadding = {
  right?: number;
  left?: number;
  top?: number;
  bottom?: number;
};

export function Padding({ right, left, top, bottom }: IPadding);
```

```typescript title="Corner"
type ICorner = Partial<WritableInstanceProperties<UICorner>>;

export function Corner({ CornerRadius }: ICorner);
```

```typescript title="ListLayout"
type IListLayout = Partial<WritableInstanceProperties<UIListLayout>>;

export function ListLayout({
  FillDirection,
  HorizontalAlignment,
  Padding,
  SortOrder,
  VerticalAlignment,
}: IListLayout);
```

```typescript title="Button"
type IButton = BaseProps<TextButton> & {
  ButtonText: string;
  Color?: ColorSequence;
  StrokeColor?: Color3;
  AspectRatio?: number;
  Clicked?: () => void;
};

export function Button({
  Position,
  Size,
  ButtonText,
  TextColor3,
  BackgroundTransparency,
  Color,
  StrokeColor,
  AspectRatio: IAspectRatio,
  Clicked,
}: IButton);
```

```typescript title="TextInput"
type ITextInput = BaseProps<TextBox> & { setText?: (text: string) => void };

export function TextInput({
  Name,
  Position,
  Size,
  Text,
  PlaceholderText,
  TextColor3,
  ClearTextOnFocus,
  setText,
}: ITextInput);
```

```typescript title="ScrollingFrame"
type IScrollingFrame = Roact.PropsWithChildren<
  BaseProps<ScrollingFrame> & { AspectRatio: number }
>;

export function ScrollingFrame({
  Position,
  Size,
  BackgroundTransparency,
  AspectRatio: IAspectRatio,
  children,
}: IScrollingFrame);
```

```typescript title="ProgressBar"
type IProgressBar = BaseProps<Frame> & {
  Size: UDim2;
  Progress: number;
  Maximum?: number;
  Color: ColorSequence;
  AspectRatio: number;
};

export function ProgressBar({
  Position,
  Size,
  Progress,
  Maximum,
  Color,
  AspectRatio: IAspectRatio,
}: IProgressBar);
```

```typescript title="BackgroundBlur"
type IBackgroundBlur = { blurSize?: number | Roact.Binding<number> };

export function BackgroundBlur({ blurSize }: IBackgroundBlur);
```

```typescript title="DelayRender"
type IDelayRender = Roact.PropsWithChildren<{
  shouldRender: boolean;
  mountDelay?: number;
  unmountDelay?: number;
}>;

export function DelayRender({
  shouldRender,
  mountDelay = 0,
  unmountDelay = 0,
  children,
}: IDelayRender);
```

## Modals

```typescript title="Modal Context: ./client/ui/context/modal.ts"
import { Modal } from "../modals";

export const ModalContext = createContext<
  [modal: Modal, setModal: (modal: Modal) => void]
>([undefined, undefined as unknown as (modal: Modal) => void]);
```

```typescript title="./client/ui/modals/index.tsx"
export * from "./codes";
export * from "./quests";
export * from "./settings";

export type IModal = { Visible: boolean };
export type Modal =
  | "Codes"
  | "Quests"
  | "Settings"
  | "Inventory"
  | "Shop"
  | "Crafting"
  | undefined;

export const Modals: {
  Component: ({ Visible }: IModal) => Element;
  Name: string;
}[] = [
  { Name: "Codes", Component: Codes },
  { Name: "Settings", Component: Settings },
  { Name: "Quests", Component: Quests },
];

export function ModalProvider() {
  const [openModal, setOpenModal] = useContext(ModalContext);

  return (
    <>
      {Modals.map((Modal) => (
        <Modal.Component Visible={openModal === Modal.Name} />
      ))}
    </>
  );
}
```

```typescript title="Modal"
type IModal = Roact.PropsWithChildren<
  BaseProps<ImageLabel> & {
    Name: string;
    RingColor: ColorSequence;
    Color: ColorSequence;
  }
>;

export function Modal({ Name, Image, Color, RingColor, children }: IModal);
```

```typescript title="Ring"
type IRing = BaseProps<ImageLabel> & {
  Color: ColorSequence;
  AspectRatio?: number;
  Image?: string;
};

export function Ring({
  Position,
  Size,
  Color,
  AspectRatio: IAspectRatio,
  Image,
}: IRing);
```

```typescript title="Header"
type IHeader = { Title: string; Color: ColorSequence };

function Header({ Title, Color }: IHeader);
```

```typescript title="Close"
function Close();
```
