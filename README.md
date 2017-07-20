# YUFoldingTableView
可快速集成UITableView的折叠cell
# [详情请参考简书](http://www.jianshu.com/p/fa8e80766529)

#效果：
![Aaron Swartz](https://github.com/XuanYuLin/YUFoldingTableView/raw/master/YUFoldingTableViewDemo/效果图/效果图.gif)
# 使用步骤
## 1.导入头文件，遵守协议

```
#import "ViewController.h"
#import "YUFoldingTableView.h"
@interface ViewController () <YUFoldingTableViewDelegate>
@property (nonatomic, weak) YUFoldingTableView *foldingTableView;
@end
```
## 2.创建YUFoldingTableView
```
    self.automaticallyAdjustsScrollViewInsets = NO;
	YUFoldingTableView *foldingTableView = [[YUFoldingTableView alloc] initWithFrame:CGRectMake(0, 64, [UIScreen mainScreen].bounds.size.width, [UIScreen mainScreen].bounds.size.height - 64)];
    _foldingTableView = foldingTableView;
    [self.view addSubview:foldingTableView];
    foldingTableView.foldingDelegate = self;
    // 可以设置cell默认展开，不设置的话，默认折叠
    foldingTableView.foldingState = YUFoldingSectionStateShow;
```
## 3.实现YUFoldingTableView的代理，用法和UItableView类似
```
#pragma mark - YUFoldingTableViewDelegate / required（必须实现的代理）
// 返回箭头的位置
- (YUFoldingSectionHeaderArrowPosition)perferedArrowPositionForYUFoldingTableView:(YUFoldingTableView *)yuTableView
{
    return YUFoldingSectionHeaderArrowPositionLeft;
}
- (NSInteger )numberOfSectionForYUFoldingTableView:(YUFoldingTableView *)yuTableView
{
    return 5;
}
- (NSInteger )yuFoldingTableView:(YUFoldingTableView *)yuTableView numberOfRowsInSection:(NSInteger )section
{
    return 3;
}
- (CGFloat )yuFoldingTableView:(YUFoldingTableView *)yuTableView heightForHeaderInSection:(NSInteger )section
{
    return 50;
}
- (CGFloat )yuFoldingTableView:(YUFoldingTableView *)yuTableView heightForRowAtIndexPath:(NSIndexPath *)indexPath
{
    return 50;
}
- (NSString *)yuFoldingTableView:(YUFoldingTableView *)yuTableView titleForHeaderInSection:(NSInteger)section
{
    return [NSString stringWithFormat:@"Title %ld",section];
}
- (UITableViewCell *)yuFoldingTableView:(YUFoldingTableView *)yuTableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    static NSString *cellID = @"cellID";
    UITableViewCell *cell = [yuTableView dequeueReusableCellWithIdentifier:cellID];
    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:cellID];
    }
    cell.textLabel.text = [NSString stringWithFormat:@"Row %ld",indexPath.row];
    return cell;
}

- (void )yuFoldingTableView:(YUFoldingTableView *)yuTableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{
    [yuTableView deselectRowAtIndexPath:indexPath animated:YES];
}

#pragma mark - YUFoldingTableViewDelegate / optional （可选择实现的）
- (NSString *)yuFoldingTableView:(YUFoldingTableView *)yuTableView descriptionForHeaderInSection:(NSInteger )section
{
    return @"detailText";
}
