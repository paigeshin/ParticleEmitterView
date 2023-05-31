# ParticleEmitterView

```swift
struct ParticleEmitterView: UIViewRepresentable {
    func makeUIView(context: Context) -> UIView {
        let view = UIView()
        let emitterLayer = createEmitterLayer()
        view.layer.addSublayer(emitterLayer)
        return view
    }

    func updateUIView(_ uiView: UIView, context: Context) {
    }

    private func createEmitterLayer() -> CAEmitterLayer {
        let emitterLayer = CAEmitterLayer()
        emitterLayer.emitterShape = .rectangle
        emitterLayer.emitterSize = CGSize(width: 360, height: 240)
        emitterLayer.emitterPosition = CGPoint(x: 180, y: 120)
        emitterLayer.renderMode = .oldestFirst // Update this line
        emitterLayer.emitterCells = createEmitterCells()
        return emitterLayer
    }

    private func createEmitterCells() -> [CAEmitterCell] {
        let numberOfEmitters = 40
        return (0..<numberOfEmitters).map { index in
            let emitterCell = createEmitterCell()
            let emissionLongitude = Double(index) * (2 * Double.pi) / Double(numberOfEmitters)
            emitterCell.emissionLongitude = CGFloat(emissionLongitude)
            emitterCell.birthRate = 5 // Update this line
            emitterCell.velocity = 50 // Update this line
            emitterCell.lifetime = 1.5 // Update this line
            return emitterCell
        }
    }

    private func createEmitterCell() -> CAEmitterCell {
        let emitterCell = CAEmitterCell()

        // Custom white circle image
        let renderer = UIGraphicsImageRenderer(size: CGSize(width: 20, height: 20))
        let whiteCircle = renderer.image { context in
            UIColor.white.setFill()
            context.cgContext.fillEllipse(in: CGRect(x: 0, y: 0, width: 20, height: 20))
        }
        emitterCell.contents = whiteCircle.cgImage

        emitterCell.birthRate = 1
        emitterCell.lifetime = 1.0
        emitterCell.scale = 0.1
        emitterCell.scaleRange = 0.02
        emitterCell.scaleSpeed = -0.05
        emitterCell.velocity = 40
        emitterCell.velocityRange = 10
        emitterCell.yAcceleration = 0
        emitterCell.alphaRange = 0.5
        emitterCell.alphaSpeed = -0.5
        return emitterCell
    }
}

```
