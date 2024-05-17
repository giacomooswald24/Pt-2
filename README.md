using GameDev.Utilities;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;
using Microsoft.Xna.Framework.Content;

namespace GameDev.Exercises
{
    class CurrentScoreObject : SceneObject
    {
        private const float _posX = 1000.0f;
        private const float _posY = 60.0f;
        private const float _spriteHalfWidth = 256.0f * 0.5f;
        private const float _spriteHalfHeight = 128.0f * 0.5f;
        private const float _scoreTextOffsetX = -60.0f;
        private const float _scoreTextOffsetY = -37.0f;

        private SpriteFont _font;

        private int _score = 0;

        private string _scoreText = "0";

        private SceneObject _scoreObject;

        public CurrentScoreObject(GraphicsDevice graphics, ContentManager content, Effect pointSpriteEffect, string name, SpriteFont font)
            : base(name)
        {
            _font = font;

            PointSprite scoreSprite = new PointSprite(graphics, pointSpriteEffect, GameTextures.HeaderScoreTexture);
            scoreSprite.Size = new Vector2(_spriteHalfWidth, _spriteHalfHeight);
            _scoreObject = new SceneObject(scoreSprite);
            _scoreObject.WorldMatrix = Matrix.CreateTranslation(new Vector3(_posX, _posY, GamePlayState.ZPositionMidground));
        }

        public override void OnAddedToSceneManager(SceneObjectManager manager)
        {
            base.OnAddedToSceneManager(manager);

            manager.AddObject(_scoreObject);
        }

        public override void OnRemovedFromSceneManager(SceneObjectManager manager)
        {
            base.OnRemovedFromSceneManager(manager);

            manager.RemoveObject(_scoreObject);
        }

        public void SetScore(int score)
        {
            _score = score;
            _scoreText = score.ToString();
        }

        public override void RenderText(GraphicsDevice graphicsDevice, SpriteBatch spriteBatch)
        {
            DrawShadowedText(spriteBatch, _font, _scoreText, _posX + _spriteHalfWidth + _scoreTextOffsetX, _posY + _scoreTextOffsetY);
        }
    }
}
